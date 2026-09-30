# Mathematical Formulation of the RD-PI and SMO Architecture

## 1. Rate-Dependent Prandtl-Ishlinskii (RD-PI) Operator
Classical P-I models are rate-independent and fail at moderate frequencies (>100 Hz). Our modified operator introduces a dynamic weighting function that scales with the input voltage derivative $\dot{V}(t)$.

The rate-dependent play operator $F_{r, \dot{V}}$ with threshold $r$ is defined as:
$$ F_{r, \dot{V}}[V](t) = \max \left( V(t) - r(\dot{V}), \min(V(t) + r(\dot{V}), x(t-\Delta t)) \right) $$

Where the threshold expands based on driving frequency to account for domain-wall friction:
$$ r(\dot{V}) = r_0 + \gamma |\dot{V}(t)| $$

The total actuator displacement $x(t)$ is integrated across the density function $p(r)$:
$$ x(t) = \int_0^R p(r) F_{r, \dot{V}}[V](t) dr $$

## 2. Analytical Inverse Calculation
To achieve feedforward tracking, the commanded trajectory $x_{cmd}(t)$ is inverted to solve for the required pre-distorted voltage $V_{pre}(t)$. The inverse density function $q(r')$ is mapped analytically to ensure execution under 4.0 µs:
$$ V_{pre}(t) = \int_0^{R'} q(r') F_{r', \dot{x}}[x_{cmd}](t) dr' $$

## 3. Sliding-Mode Observer (SMO) Feedback
To suppress thermal drift and residual modeling error $e(t) = x_{cmd}(t) - x(t)$, the SMO injects a discontinuous high-frequency switching control signal $u_{smo}(t)$:
$$ u_{smo}(t) = -K \cdot \text{sgn}(\sigma(t)) $$
Where $\sigma(t) = \dot{e}(t) + \lambda e(t)$ is the sliding surface. This guarantees asymptotic stability as $t \rightarrow \infty$ despite bounded external disturbances.
