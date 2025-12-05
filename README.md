# MuJoCo STL Mesh Fixer & Decimator

A lightweight Python utility designed to batch process STL mesh files for robotics simulations (MuJoCo, Gazebo, PyBullet). 

It automatically fixes common **URDF compilation errors** by converting ASCII STLs to Binary and reducing polygon counts (decimation) while preserving mesh topology.

## 🚀 Why use this?

If you are trying to compile a URDF in MuJoCo (`./compile`) and see errors like this:

> **Error:** number of faces should be between 1 and 200000 in STL file... perhaps this is an ASCII file?

This script solves it in seconds by:
1.  **Converting Format:** Automatically converts ASCII STLs to **Binary STL** (required by MuJoCo's reader).
2.  **Reducing Faces:** Checks if the mesh exceeds a maximum face count (default: 150k) and applies **Quadric Edge Collapse Decimation** to simplify it without losing shape details.

## 📋 Prerequisites

You need Python installed and the `pymeshlab` library.

```bash
pip install pymeshlab
```

## 🛠 Usage

1.  **Download** the `fix_meshes.py` script.
2.  **Place** the script directly inside the folder containing your `.STL` files (e.g., `your_robot_description/meshes/`).
3.  **Run** the script:

```bash
cd /path/to/your/meshes/
python fix_meshes.py
```

5.  Re-run your MuJoCo compilation command (`./compile`).

## ⚙️ Configuration

You can open the script and modify the configuration section at the top:

```python
# Configuration
# ----------------------------------------
MAX_FACES = 150000   # Max allowed faces (MuJoCo limit is ~200k)
OVERWRITE = True     # Set to False to save as 'filename_fixed.stl' instead
# ----------------------------------------
```

## 📝 How it Works

* **Library:** Uses `pymeshlab` (Python bindings for MeshLab) for robust geometric processing.
* **Algorithm:** Uses "Quadric Edge Collapse Decimation" for simplification. This is superior to simple vertex clustering as it preserves sharp edges and boundaries essential for accurate collision detection.

## ⚠️ Note

* **Backup:** Although the script is safe, it is always recommended to backup your original `meshes` folder before running batch operations, especially if `OVERWRITE = True`.

## License

MIT License. Feel free to use and modify for your robotics projects.
