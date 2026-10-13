# edgewise

Releases of **edgewise**, a command-line tool for surface meshes, built for
the meshes real tools export and for what comes after them: simulation and
3D printing. Slivers, cracks, flipped faces, holes, overlapping parts and
self-intersections go in; clean, even triangles or quads that stay true to
the original shape come out.

## Download

Get the archive for your platform from the
[releases](https://github.com/vijaiaeroastro/edgewise-releases/releases):
Linux, macOS and Windows, on x86-64 (`amd64`) and ARM (`arm64`). Each holds
the `edgewise` binary, with no dependencies, and its manual. `SHA256SUMS`
lists the archives' checksums:

```
sha256sum -c SHA256SUMS --ignore-missing
```

## What it does

```
edgewise info part.stl                           # parts, holes, crossings, quality
edgewise repair scan.stl clean.stl               # fill holes, remove crossings
edgewise remesh part.stl even.stl -size 2        # even triangles
edgewise remesh part.stl quads.obj -size 1% -quads
edgewise wrap broken.stl closed.stl -alpha 0.5%  # a valid solid from anything
edgewise denoise scan.stl smooth.stl             # remove noise, keep sharp edges
edgewise hollow part.stl shell.stl -wall 2 -drain 0,0,0,1.5
```

Also `cut`, `defeature`, `thickness`, `boolean`, `assemble`, `reconstruct` and
`convert`; `license` prints the license and `version` the version.
`edgewise -h` lists the commands, and `edgewise <command> -h` a command's
flags. Files are STL, OBJ, OFF or PLY.

## License

edgewise is closed source; see [LICENSE](LICENSE). The binaries here are
free for non-commercial use: personal use, teaching and academic research.
Commercial use is not licensed; for anything beyond non-commercial use,
contact vijai@meshing.engineer.
