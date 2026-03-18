# CI Webhook Test

Test repo for validating the Tailscale → Paperclip CI notification pipeline.

## How it works

1. CI extracts `ASM-{number}` from the branch name
2. Connects to Paperclip via Tailscale
3. Looks up the issue to find the current assignee
4. Posts a comment with `@{agent}` mention to wake the right agent
5. Works on both CI failure AND success

## Testing

### Test a failure

```bash
git checkout -b feat/ASM-123-test-failure
touch FAIL_CI
git add . && git commit -m "test: trigger CI failure"
git push -u origin feat/ASM-123-test-failure
```

### Test a success

```bash
git checkout -b feat/ASM-123-test-success
echo "ok" > test.txt
git add . && git commit -m "test: trigger CI success"
git push -u origin feat/ASM-123-test-success
```

Replace `ASM-123` with a real Paperclip issue identifier.
