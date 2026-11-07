# Betti

Releases of **Betti**, a command-line tool that prepares geometry for
simulation and manufacturing. It repairs the meshes real tools export
(slivers, cracks, flipped faces, holes, overlapping parts and
self-intersections), remeshes them into clean, even triangles or quads that
stay true to the original shape, heals and meshes CAD models, fills solids
with tetrahedra, polyhedra or hexahedra, and checks parts for 3D printing
and other manufacturing processes. It runs one command at a time, as
scripts, or from a coding agent.

Documentation, examples and downloads: **[betti.dev](https://betti.dev)**.

## Download

Get the archive for your platform from the
[releases](https://github.com/vijaiaeroastro/betti-releases/releases):
Linux, macOS and Windows, on x86-64 (`amd64`) and ARM (`arm64`). Each holds
the `betti` executable, with no dependencies, and its licence. `SHA256SUMS`
lists the archives' checksums:

```
sha256sum -c SHA256SUMS --ignore-missing
```

## What it does

```
betti info part.stl                                    # parts, holes, crossings, quality
betti fix repair part.stl clean.3mf                    # fill holes, remove crossings
betti mesh remesh -size 2 part.stl even.obj            # even triangles
betti mesh remesh -size 1% -quads part.stl quads.obj   # quads
betti fix wrap -gap 0.5% broken.stl closed.obj         # a valid solid from anything
betti shape hollow -wall 2 -drain 0,0,0,1.5 part.stl shell.3mf
betti cad mesh -size 2 part.step part.vtu              # STEP to triangles tagged by CAD face
betti volume tet -size 2% clean.3mf part.msh           # tetrahedra for FEA
betti dfm check -process machining part.step           # manufacturability
betti verify part.stl even.obj                         # how far the result is from the input
```

Flags come before the files. Lengths are absolute, or a percentage of the
part's size, as in `-size 1%`.

**Chains, scripts and agents.** `betti run` passes a mesh from step to step
in memory:

```
betti run part.stl prepared.obj fix repair + mesh remesh -size 1%
```

`betti script` runs scripts in Starlark, a small language that reads like
Python, with every command as a function, for loops over parts and
decisions on what a command reports:

```python
for path in args:
    m = mesh.remesh(fix.repair(path), size = "1%")
    print(path, m.faces, info(m).holes)
    save(m, path.removesuffix(".stl") + ".obj")
```

`betti mcp` gives coding agents such as Claude Code, Codex and Copilot every
command as a tool: `claude mcp add betti -- betti mcp`.

**Modules.** Core commands (`info`, `box`, `verify`, `convert`, `run`,
`script`, `mcp`) are free and need no account. The others are grouped by
module (`fix`, `mesh`, `shape`, `cad`, `volume`, `dfm`, `additive` and
`particles`), each granted on request: `betti access` shows them and
`betti access request MODULE` asks for one. `betti help` lists the
commands, `betti <module>` a module's, and `betti help <module> <command>`
a command's flags and examples.

**Formats.** Meshes are read from OBJ, OFF, PLY, Gmsh, VTK, 3MF, JT,
Nastran and STL, and written to all but STL. CAD models are read from
STEP, IGES, JT and Parasolid. Volume meshes are written for Gmsh, VTK,
Abaqus, Nastran and OpenFOAM.

## License

Betti is closed source; see [LICENSE](LICENSE). The executables here are
free for non-commercial use: personal use, teaching and academic research.
Commercial use is not licensed, and there is no commercial offering.
Because of the author's employment and possible conflicts of interest, a
request for use beyond these terms is considered only rarely, case by
case, and most will be declined; if your case is exceptional, write to
vijai@meshing.engineer.

Betti was called edgewise up to v0.17.
