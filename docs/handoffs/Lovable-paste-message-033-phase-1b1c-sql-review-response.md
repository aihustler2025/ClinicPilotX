# Lovable Paste Message 033 - Phase 1B.1c SQL Review Response

Date: 2026-06-26

Use this in Lovable Plan mode only. Do not build yet.

```text
Codex reviewed the Phase 1B.1c Internal Chat Fix Plan.

Directionally approved:
- Fixing the internal chat recursion/channel creation problem is the right next step.
- Keeping scheduled_messages, live sends, payments, edge functions, Automation Center, Settings, Subscription, and Phase 1B.2 read filtering out of scope is correct.
- Using a server-side RPC for DM creation makes sense because the client cannot safely create both channel-member rows under the current policies.

Do not run the migration yet. Please revise the SQL plan first with these changes:

1. Make the membership helper safer.

Instead of:

public.is_internal_channel_member(_channel_id uuid, _user_id uuid)

prefer a one-argument helper that checks the current authenticated user only:

public.is_internal_channel_member(_channel_id uuid)

The helper should use auth.uid() internally. This avoids exposing a function that lets an authenticated user probe whether some other user belongs to a private channel.

Use it in policies as:

public.is_internal_channel_member(id)
public.is_internal_channel_member(channel_id)

2. Add an explicit caller membership check inside create_dm_channel.

After _clinic := public.current_clinic_id(), add a direct check that the caller is a member of that clinic:

IF NOT public.is_clinic_member(_clinic) THEN
  RAISE EXCEPTION 'Caller is not a member of this clinic';
END IF;

Do not rely only on active_clinic_id existing.

3. Tighten internal_messages INSERT policy so message clinic_id matches the channel clinic_id.

The INSERT policy should require:
- sender_id = auth.uid()
- the sender is a member of the channel
- clinic_id IS NOT NULL
- clinic_id equals the clinic_id of the referenced internal_channels row

Example intent:

clinic_id = (
  SELECT ic.clinic_id
  FROM public.internal_channels ic
  WHERE ic.id = channel_id
)

This keeps Phase 1B clinic_id stamping honest at the database layer, not only in the frontend.

4. Use DROP POLICY IF EXISTS where appropriate.

Lovable says these policies exist, but use IF EXISTS to avoid a failed migration if the live policy name differs slightly or has already been adjusted.

5. Confirm create_dm_channel returns only a channel id and does not expose private channel/member data.

The frontend can fetch the channel normally afterward through the corrected policies.

6. Provide the revised exact SQL again before build approval.

After you revise the SQL, respond in Plan mode only with:
- the final SQL migration,
- exact frontend changes in InternalChat.tsx,
- rollback SQL,
- QA plan,
- confirmation that scheduled_messages and all send-capable paths remain untouched.

Do not build or run SQL until Codex reviews the revised exact SQL.
```

