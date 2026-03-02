# AGENTS.md

## Cursor Cloud specific instructions

This is a MuJoCo robotics simulation tutorial repository (Python). There are no build tools, no package managers (no `requirements.txt` or `pyproject.toml`), and no external services required.

### Dependencies

All Python packages are installed globally via pip: `mujoco`, `numpy`, `matplotlib`, `mediapy`, `jax`, `jaxlib`, `casadi`, `jupyter`, `ipykernel`.

### Running notebooks

- Use `jupyter nbconvert --to notebook --execute <notebook>.ipynb` to run notebooks headlessly.
- `optimization.ipynb` executes cleanly end-to-end.
- `mujoco_basic.ipynb` and `robot_arms.ipynb` fail on some cells due to MuJoCo 3.x API breaking changes (e.g., `mjv_makeConnector` removed, `data.joint().qpos` changed). These are existing code issues, not environment problems.
- `direct_transcription_method.ipynb` is explicitly "Work in Progress" and does not complete.
- `robot_arm_mocap.py` requires a GUI display (GLFW/X11) and cannot run in headless environments.

### Headless rendering

Environment variable `MUJOCO_GL=egl` is set in `~/.bashrc` for headless GPU-accelerated rendering. Three backends are available:
- `egl` (default, recommended for headless) — no display needed
- `osmesa` — pure software rendering, no display needed
- `glfw` — also works in this VM (Xvfb available), but primarily for GUI use

Use `mujoco.Renderer` for offscreen rendering. Use `matplotlib.use('Agg')` when saving plots non-interactively.

### Linting

Run `python3 -m pyflakes robot_arm_mocap.py` for basic lint checks on the Python file. There is no formal linting configuration in this repo.
