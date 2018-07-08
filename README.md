
# Verification


```python
# Verification Example
from ecc import G, N, S256Point

z = 0xbc62d4b80d9e36da29c16c5d4d9f11731f36052c72401a76c23c0fb5a9b74423
r = 0x37206a0610995c58074999cb9767b87af4c4978db68c06e8e6e81d282047a7c6
s = 0x8ca63759c1157ebeaec0d03cecca119fc9a75bf8e6d0fa65c841c8e2738cdaec
point = S256Point(0x04519fac3d910ca7e7138f7013706f619fa8f033e6ec6e09370ea38cee6a7574,
                  0x82b51eab8c27c66e26c858a079bcdf4f1ada34cec420cafc7eac1a42216fb6c4)
u = z * pow(s, N-2, N) % N
v = r * pow(s, N-2, N) % N
print((u*G + v*point).x.num == r)
```

### Try it

#### Which sigs are valid?

```
P = (887387e452b8eacc4acfde10d9aaf7f6d9a0f975aabb10d006e4da568744d06c, 
     61de6d95231cd89026e286df3b6ae4a894a3378e393e93a0f45b666329a0ae34)
z, r, s = ec208baa0fc1c19f708a9ca96fdeff3ac3f230bb4a7ba4aede4942ad003c0f60,
          ac8d1c87e51d0d441be8b3dd5b05c8795b48875dffe00b7ffcfac23010d3a395,
          68342ceff8935ededd102dd876ffd6ba72d6a427a3edb13d26eb0781cb423c4
z, r, s = 7c076ff316692a3d7eb3c3bb0f8b1488cf72e1afcd929e29307032997a838a3d,
          eff69ef2b1bd93a66ed5219add4fb51e11a840f404876325a1e8ffe0529a2c,
          c7207fee197d27c618aea621406f6bf5ef6fca38681d82b2f06fddbdce6feab6
```


```python
from ecc import S256Point, G, N

px = 0x887387e452b8eacc4acfde10d9aaf7f6d9a0f975aabb10d006e4da568744d06c
py = 0x61de6d95231cd89026e286df3b6ae4a894a3378e393e93a0f45b666329a0ae34

signatures = (
    # (z, r, s)
    (0xec208baa0fc1c19f708a9ca96fdeff3ac3f230bb4a7ba4aede4942ad003c0f60,
     0xac8d1c87e51d0d441be8b3dd5b05c8795b48875dffe00b7ffcfac23010d3a395,
     0x68342ceff8935ededd102dd876ffd6ba72d6a427a3edb13d26eb0781cb423c4),
    (0x7c076ff316692a3d7eb3c3bb0f8b1488cf72e1afcd929e29307032997a838a3d,
     0xeff69ef2b1bd93a66ed5219add4fb51e11a840f404876325a1e8ffe0529a2c,
     0xc7207fee197d27c618aea621406f6bf5ef6fca38681d82b2f06fddbdce6feab6),
)

# initialize the public point
# use: S256Point(x-coordinate, y-coordinate)

# iterate over signatures
    # u = z / s, v = r / s
    # finally, uG+vP should have the x-coordinate equal to r
```

## Test Driven Exercise


```python
from ecc import Signature

class S256Point(S256Point):

    def verify(self, z, sig):
        # remember sig.r and sig.s are the main things we're checking
        # remember 1/s = pow(s, N-2, N)
        # u = z / s
        # v = r / s
        # u*G + v*P should have as the x coordinate, r
        pass
```
