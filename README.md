# Strange Attractor Synth

**Find my Audiovisual projects on http://gumroad.com/tmhglnd**

**Consider to become a patron on http://patreon.com/timohoogland**

# About

This patch uses the xyz coordinates of a Strange Attractor chaotic system to modulate parameters from an FM synthesizer with resonant lowpass filter and flanger effects. Various different Strange Attractors are programmed in the gen~ patcher with codebox (such as the famous Lorenz Attractor). The attractor can be selected in the umenu and is displayed in the openGL domain using jit.catch~ and jit.gl.path, and also through 4 phase-correlation scopes showing the x-y, y-z, x-z and distance to origin of the signal. Listening to the pure modulation signal is also possible. The coordinates of the attractor are output from the gen~ as a 3-channel signal.

# Sources

https://en.wikipedia.org/wiki/Lorenz_system

https://en.wikipedia.org/wiki/Multiscroll_attractor

https://www.deviantart.com/chaoticatmospheres/gallery/44050549/strange-attractors

# Included Attractors

- Lorenz Attractor
- Lorenz Mod 2 Attractor
- Aizawa Attractor
- Arneodo Attractor
- Burke-Shaw Attractor
- Chen-Lee Attractor
- Thomas Attractor
- Hadley Attractor
- Halvorsen Attractor
- Thee-Scroll Unified Chaotic System Attractor
- Coullet Attractor
- Dadras Attractor

## Strange Attractor Formulas

The basis method for all attractors is the following pseudocode
```
dt = 0.01;

x = x + dt * attractormethodX();
y = y + dt * attractormethodY();
z = z + dt * attractormethodZ();
```

### Lorenz Attractor
```
// dx/dt = a(y-x)
// dy/dt = x(b-z)
// dz/dt = xy-bz

a = 10;
b = 28;
c = 8/3;

x = x + dt * (a * (y - x));
y = y + dt * (x * (b - z) - y);
z = z + dt * (x * y - c * z);
```
<!--
### Lorenz Mod 1 Attractor
```
// dx/dt = -ax+y^2-z^2+ac
// dy/dt = x(y-bz)+d
// dz/dt = z+x(by+z)

a = 0.1;
b = 4;
c = 14;
d = 0.08;

x = x + dt * (-a * x + (y*y) - (z*z) + a * c);
y = y + dt * (x * (y - b * z) + d);
z = z + dt * (z + x * (b * y + z));
``` 
-->
### Lorenz Mod 2 Attractor
```
// dx/dt = -ax+y^2-z^2+ac
// dy/dt = x(y-bz)+d
// dz/dt = -z+x(by+z)

a = 0.9;
b = 5;
c = 9.9;
d = 1;

x = x + dt * (-a * x + (y*y) - (z*z) + a * c);
y = y + dt * (x * (y - b * z) + d);
z = z + dt * (-z + x * (b * y + z));
```

### Aizawa Attractor
```
// dx/dt = (z-b)x-dy 
// dy/dt = dx+(z-b)y 
// dz/dt = f+az-(z^3/3)-(x^2+y^2)(1+ez)+czx^3

a = 0.95;
b = 0.7;
c = 0.1;
d = 3.5;
e = 0.25;
f = 0.6;

x = x + dt * ((z - b) * x - d * y);
y = y + dt * (d * x + (z - b) * y);
z = z + dt * (f + a * z - (z*z*z)/3 - (x*x + y*y) * (1 + e*z) + c * z * (x*x*x));
```

### Arneodo Attractor
```
// dx/dt = y
// dy/dt = z
// dz/dt = -ax-by-z+d(x^3)

a = -5.5;
b = 3.5;
c = -1;

x = x + dt * y;
y = y + dt * z;
z = z + dt * (-a * x - b * y - z + c * pow(x, 3));
```

### Burke-Shaw Attractor
```
// dx/dt = -c(x+y)
// dy/dt = -y-cxz
// dz/dt = sxy+v

a = 10;
b = 4.272;

x = x + dt * (-a * (x + y));
y = y + dt * (-y - a * x * z);
z = z + dt * (a * x * y + b);
```
<!--
Needs Fixing

### Chen - Celikovsky Attractor
```
// dx/dt = a(y-x)
// dy/dt = -xz+cy
// dz/dt = xy-bz

a = 36;
b = 3;
c = 20;

x = x + dt * (a * (y - x));
y = y + dt * (-x * z + c * y);
z = z + dt * (x * y - b * z);
```
-->
### Chen-Lee Attractor
```
// dx/dt = ax-yz
// dy/dt = by+xz
// dz/dt = cz+x(y/3)

a = 5;
b = -10;
c = -0.38;

x = x + dt * (a * x - y * z);
y = y + dt * (b * y + x * z);
z = z + dt * (c * z + x * (y / 3));
```

### Thomas Attractor
```
// dx/dt = bx+sin(y)
// dy/dt = -by+sin(z)
// dz/dt = -bz+sin(x)

a = 0.19

x = x + dt * (a * x + sin(y));
y = y + dt * (-a * y + sin(z));
z = z + dt * (-a * z + sin(x));
```

### Hadley Attractor
```
// dx/dt = -y^2-z^2-ax+ac
// dy/dt = xy-bxz-y+d
// dz/dt = bxy+xz-z

a = 0.2;
b = 4;
c = 8;
d = 1;

x = x + dt * (-(y*y) - (z*z) - a * x + a * c);
y = y + dt * (x * y - b * x * z - y + d);
z = z + dt * (b * x * y + x * z - z);
```

### Halvorsen Attractor
```
// dx/dt = -ax-4y-4z-y^2
// dy/dt = -ay-4z-4x-z^2
// dz/dt = -az-4x-4y-x^2

a = 1.4;

x = x + dt * (-a*x - 4*y - 4*z - y*y);
y = y + dt * (-a*y - 4*z - 4*x - z*z);
z = z + dt * (-a*z - 4*x - 4*y - x*x);
```

### Three-Scroll Unified Chaotic System Attractor
```
// dx/dt = a(y-x)+dxz
// dy/dt = cy-xz
// dz/dt = bz+xy-fx^2

a = 40;
b = 0.833;
c = 20;
d = 0.5;
f = 0.65

x = x + dt * (a * (y - x) + d*x*z);
y = y + dt * (c*y - x*z);
z = z + dt * (b*z + x*y - f * (x*x));
```

### Coullet Attractor
```
// dx/dt = y
// dy/dt = z
// dz/dt = ax+by+cz+dx^3

a = 0.8;
b = -1.1;
c = -0.45
d = -1;

x = x + dt * (y);
y = y + dt * (z);
z = z + dt * (a*x + b*y + c*z + d*(x*x*x));
```

### Dadras Attractor
```
// dx/dt = y-px+oyz
// dy/dt = ry-xz+z
// dz/dt = cxy-sz

a = 3;
b = 2.7;
c = 1.7;
d = 2;
f = 9;

x = x + dt * (y - a*x + b*y*z);
y = y + dt * (c*y - x*z + z);
z = z + dt * (d*x*y - f*z);
```