# Betti

Releases of **Betti**, a command-line tool for surface meshes and CAD
geometry, built for the meshes and models real tools export and for what
comes after them: simulation and 3D printing. Slivers, cracks, flipped
faces, holes, overlapping parts and self-intersections go in; clean, even
triangles or quads that stay true to the original shape come out. STEP
models are checked for defects and meshed watertight, each triangle
tagged with its CAD face.

Betti was called edgewise up to v0.17.

## Download

Get the archive for your platform from the
[releases](https://github.com/vijaiaeroastro/betti-releases/releases):
Linux, macOS and Windows, on x86-64 (`amd64`) and ARM (`arm64`). Each holds
the `betti` binary, with no dependencies, and its licence. `SHA256SUMS`
lists the archives' checksums:

```
sha256sum -c SHA256SUMS --ignore-missing
```

## What it does

```
betti info part.stl                              # parts, holes, crossings, quality
betti fix repair scan.stl clean.3mf              # fill holes, remove crossings
betti mesh remesh part.stl even.obj -size 2      # even triangles
betti mesh remesh part.stl quads.obj -size 1% -quads
betti fix wrap broken.stl closed.obj -alpha 0.5% # a valid solid from anything
betti shape hollow part.stl shell.3mf -wall 2 -drain 0,0,0,1.5
betti cad mesh part.step part.vtu -size 2        # STEP to well-shaped triangles
```

Core commands (`info`, `verify`, `box`, `convert`, `run`) are free; the
others are grouped by module, `fix`, `mesh`, `shape`, `cad`, `additive`
and `particles`, each available on request: `betti access` shows them and
`betti access request MODULE` asks for one. `betti help` lists the
commands, `betti <module>` a module's, and `betti help <module> <command>`
a command's flags. Meshes are read from OBJ, OFF, PLY, Gmsh .msh, VTK .vtu,
3MF and STL, and written to all but STL.

## License

Betti is closed source; see [LICENSE](LICENSE). The binaries here are
free for non-commercial use: personal use, teaching and academic research.
Commercial use is not licensed; for anything beyond non-commercial use,
contact vijai@meshing.engineer.
