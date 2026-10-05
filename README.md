# marthofdoom vcpkg registry

A small vcpkg git registry for SKSE plugins. It holds one port.

- `commonlibsse-ng` builds the MIT line of CommonLibSSE-NG 3.7.0 from
  [marthofdoom/CommonLibSSE-NG](https://github.com/marthofdoom/CommonLibSSE-NG), branch `main`.

## What it serves today

| port | version | fork commit |
|---|---|---|
| `commonlibsse-ng` | 3.7.0, port-version 19 | `11a5858be2c11f79b3259fbe1a7c4f38e03a8e13` |

That commit is CharmedBaryon's 3.7.0, plus the fixes verified on the game's own code, the upstream MIT commits up
to 2024-09, and Skyrim SE 1.7.104 support. The fork's README lists every change and the proof behind it.

Supported game versions:

| game version | ids come from |
|---|---|
| 1.5.97.0 | the Address Library, `version-1-5-97-0.bin` |
| 1.6.1170.0 | the Address Library, `versionlib-1-6-1170-0.bin` |
| 1.7.104.0 (Steam) | the fork's own id table, `Data/SKSE/Plugins/mit-idtable-v1-1-7-104-0.bin`, a separate download the plugin lists as a requirement |

Other builds are not verified. See the fork's README for exactly what each one does.

## Using it

The port name matches the upstream one on purpose. In your project's `vcpkg-configuration.json`, send
`commonlibsse-ng` to this registry and drop any other registry entry for it. Your `vcpkg.json` and CMake stay the
same. Every other package still comes from the default registry.

```json
{
    "default-registry": {
        "kind": "git",
        "repository": "https://github.com/microsoft/vcpkg.git",
        "baseline": "<a microsoft/vcpkg commit>"
    },
    "registries": [
        {
            "kind": "git",
            "repository": "https://github.com/marthofdoom/vcpkg-registry",
            "baseline": "<a commit of this repository's main>",
            "packages": [ "commonlibsse-ng" ]
        }
    ]
}
```

- `baseline` is a commit of this repository. It pins the port version, and so the exact fork commit. Use the
  newest commit of `main` to get the version in the table above.
- No `reference` is needed: vcpkg reads the version database from `main`, which is the default branch. A
  `reference` is only for testing a port from another branch.
- If your CI caches vcpkg packages, put `vcpkg-configuration.json` in the cache key, or an old build of the
  library hides the new one.

## License

The portfile is taken from the colorglass registry
([gitlab.com/colorglass/vcpkg-colorglass](https://gitlab.com/colorglass/vcpkg-colorglass), Apache-2.0) at commit
`6309841a1ce770409708a67a9ba5c26c537d2937`, port version 3.7.0. The changes are the source (`REPO`, `REF`, `SHA512`,
`HEAD_REF`) and the port metadata. The build options are unchanged. This registry is under the same Apache-2.0
license. The library it builds is MIT.
