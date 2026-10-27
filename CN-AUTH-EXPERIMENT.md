# China authentication experiment

Based on upstream v0.25.3. This fork tests the endpoint split reported in
icloud-photos-downloader/icloud_photos_downloader#1256: authenticate China
accounts through `idmsa.apple.com`, retaining `www.icloud.com.cn` and
`setup.icloud.com.cn` for iCloud service access.

Keep `[auth].domain = "cn"`. This is an experimental compatibility change,
not a confirmed fix or an Apple-supported interface. No media, state schema,
credential storage, or download behavior is changed.

GitHub Actions publishes an amd64 image to `ghcr.io/b83c/kei:0.25.3-cn-auth`
and a full-commit tag. Pin the resulting image digest for account testing.
No Apple credentials are used in CI. Back up the affected account's stopped
configuration/state directory before testing; do not run simultaneous clients
against it. Test `login` first, then a read-only library listing after 2FA.
Keep the upstream image and matched pre-test state backup for rollback.
