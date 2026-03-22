# User Guide: VFPB for OpenSeesPy

This README serves as the user guide for implementing the VFPB2Ring element and the VariableFriction2Ring friction model.

---

## 1. Environment Requirements
- **Operating system:** Windows 64-bit
- **Python version:** 3.8.x
- **OpenSeesPy version:** 3.3.0

> **Note:** The `opensees.pyd` file is compiled for Python 3.8. Compatibility with other environments should be checked separately.

---

## 2. Installation Instructions
To use the developed element, you need to replace the original OpenSeesPy binary file:

1.  **Locate the installation path:** Find the `openseespywin` directory in your Python site-packages.
    *Example:* `E:\Anaconda\envs\py3.8\Lib\site-packages\openseespywin\`
2.  **Backup:** Back up the original `opensees.pyd` file.
3.  **Replace:** Replace it with the provided `opensees.pyd` file from this repository.
4.  **Restart:** Restart Python or your IDE and run your OpenSeesPy script.

---

## 3. Friction Model: VariableFriction2Ring

### Command Syntax
```python
ops.frictionModel('VariableFriction2Ring', frnTag, r0, r1, muInSlow, muOutSlow, 
                  '-velocity1', muInFast0, transRateIn, 
                  '-velocity2', muOutFast0, transRateOut, 
                  '-pressure1', deltaMuIn, alphaIn, 
                  '-pressure2', deltaMuOut, alphaOut)
```

### Parameter Definitions
- `r0`: Slider radius.
- `r1`: Inner region radius.
- `muInSlow`: Inner-zone friction coefficient (at low velocity).
- `muOutSlow`: Outer-zone friction coefficient (at low velocity).

The velocity- and pressure-related parameters in `VariableFriction2Ring` are defined consistently with those in **Velocity and Pressure Dependent Friction** in OpenSees.

**Notes:**
- The velocity and contact-pressure effects can be applied independently to the inner and outer friction coefficients.
- These effects are ignored by default when the corresponding parameters are not specified.

---

## 4. Element: VFPB2Ring

### Command Syntax
```python
ops.element('VFPB2Ring', eleTag, *eleNodes, frnMdlTag, Reff, kInit, 
            '-P', PMatTag, '-T', TMatTag, '-My', MyMatTag, '-Mz', MzMatTag, 
            <'-orient', <x1, x2, x3>, y1, y2, y3>, 
            <'-shearDist', sDratio>, 
            <'-doRayleigh'>, 
            <'-mass', m>, 
            <'-iter', maxIter, tol>)
```

### Parameter Definitions
The `VFPB2Ring` element is developed based on the **Single Friction Pendulum Bearing** element and adopts the same parameter definitions, but additionally passes the absolute displacement to the friction model.

---
