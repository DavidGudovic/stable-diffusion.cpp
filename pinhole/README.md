# Pinhole engine build

This fork exists only to build `sd-server` for [Pinhole](https://github.com/DavidGudovic/PinholeAI)
with one small security patch. The engine code itself is upstream's, unchanged.

- `0001-server-api-key-and-reject-origin.patch` adds two opt-in options to `sd-server`:
  `--api-key` (or the `SD_API_KEY` environment variable), which requires
  `Authorization: Bearer <key>` on every request, and `--reject-origin`, which refuses requests
  from web pages (any `Origin` header). Pinhole starts the engine with a new random key each time,
  so no other program and no web page can use it.
- `.github/workflows/pinhole-build.yml` (Actions → Pinhole engine build → Run workflow) checks
  out upstream at the given tag, applies the patch, builds Linux CPU / Vulkan / CUDA and Windows
  CPU / Vulkan / CUDA, and publishes a release with the zips and `SHA256SUMS.txt`.

The source of truth for the patch is `engine/sd-cpp/` in the Pinhole repo.
