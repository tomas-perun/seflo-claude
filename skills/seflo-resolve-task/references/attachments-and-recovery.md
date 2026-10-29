# Attachments and action recovery

Read the relevant section when a task involves files or an existing action has an
uncertain outcome. Use current tool inputs and returned limits rather than copying
provider-specific payloads from old examples.

## Read, transform and select files

1. Discover task attachments with `seflo_list_task_attachments`. Read relevant
   content with `seflo_read_attachment`; extracted text is not the original file.
   Follow actual returned pagination/range information when complete bytes matter.
2. Preserve the requested original data when transforming a file. Use actual bytes
   accessible to the client, compute size and SHA-256 from those bytes, and verify
   the resulting content. Do not present a sandbox path or generated-image URL as
   an already uploaded Seflo attachment.
3. For a new file, use `seflo_begin_attachment_upload`,
   `seflo_upload_attachment_chunk` and `seflo_finalize_attachment_upload`.
   Reuse the same retry key for identical bytes, follow the returned upload progress
   and current chunk schema, and require successful finalization. This publishes
   a native task attachment in Seflo; it does not deliver the file externally.
4. Select the finalized reference in the prepared intent's attachments, using
   `type=reference` and `id` set to the returned attachment reference ID. For an
   existing task attachment, use its authorized metadata/reference and fetch its
   content first when required by its state. Private action-app file tools are
   reserved for the panel, not callable by the model. File selection must
   follow this action's limits; a connector supporting files elsewhere is not proof
   this particular action supports them.
5. Prepare and open the completed proposal. A chat download link, successful upload
   or visible draft is not evidence of external delivery. If the available client
   cannot read/transform/upload the required bytes, report the limitation and offer
   the existing action panel's upload path when supported; do not silently omit a
   requested file and call the task complete.

## Existing drafts and uncertain delivery

- Read an existing draft through `seflo_get_action_proposal`. Reopen it only when
  the user asks. Use the editable panel for changes to an existing proposal;
  do not create duplicate drafts for status checks.
- Read durable execution through `seflo_get_action_operation`. Accepted steps,
  pending steps and task completion may differ. Report that distinction.
- If delivery succeeded but completion failed, preserve the accepted delivery.
  Direct the user to the existing action's recovery controls for pending work.
  Do not prepare another send or claim that an error means nothing happened.
- A timeout is not permission to retry delivery. Inspect the existing result; if
  it cannot be determined, say so and retain the action reference for recovery.
