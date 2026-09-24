# marthofdoom vcpkg registry

A small vcpkg git registry for my SKSE plugins. It holds one port today.

- `commonlibsse-ng` builds CommonLibSSE-NG 3.7.0 kept on MIT, from
  [marthofdoom/CommonLibSSE-NG](https://github.com/marthofdoom/CommonLibSSE-NG/tree/mit-3.7) branch `mit-3.7`.

The port name matches the upstream one on purpose. A consumer points `commonlibsse-ng` at this registry in its
`vcpkg-configuration.json` and drops the colorglass entry. Its `vcpkg.json` and CMake stay the same. Every other
package still comes from the default registry.

```json
{
    "kind": "git",
    "repository": "https://github.com/marthofdoom/vcpkg-registry",
    "baseline": "<commit of this repo>",
    "packages": [ "commonlibsse-ng" ]
}
```

The portfile is taken from the colorglass registry
([gitlab.com/colorglass/vcpkg-colorglass](https://gitlab.com/colorglass/vcpkg-colorglass), Apache-2.0) at commit
`6309841a1ce770409708a67a9ba5c26c537d2937`, port version 3.7.0. The changes are the source (`REPO`, `REF`, `SHA512`,
`HEAD_REF`) and the port metadata. The build options are unchanged. This registry is under the same Apache-2.0
license. The library it builds is MIT.
