[![Stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://qiskit.github.io/QiskitIBMRuntimeC.jl/stable/)
[![Dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://qiskit.github.io/QiskitIBMRuntimeC.jl/dev/)
[![Build Status](https://github.com/Qiskit/QiskitIBMRuntimeC.jl/actions/workflows/CI.yml/badge.svg?branch=main)](https://github.com/Qiskit/QiskitIBMRuntimeC.jl/actions/workflows/CI.yml?query=branch%3Amain)
[![Coverage](https://coveralls.io/repos/github/Qiskit/QiskitIBMRuntimeC.jl/badge.svg?branch=main)](https://coveralls.io/github/Qiskit/QiskitIBMRuntimeC.jl?branch=main)
[![PkgEval](https://JuliaCI.github.io/NanosoldierReports/pkgeval_badges/Q/Qiskit.svg)](https://JuliaCI.github.io/NanosoldierReports/pkgeval_badges/Q/Qiskit.html)
[![Aqua](https://raw.githubusercontent.com/JuliaTesting/Aqua.jl/master/badge.svg)](https://github.com/JuliaTesting/Aqua.jl)

# QiskitIBMRuntimeC

Julia wrapper of [qiskit-ibm-runtime-c](https://github.com/Qiskit/qiskit-ibm-runtime-c)

### Example

```julia
using Qiskit
using QiskitIBMRuntimeC

function generate_bell_circuit()
    qc = QuantumCircuit(2, 2) # 2 qubits, 2 clbits
    qc.h(1)
    qc.cx(1, 2)
    qc.measure(1, 1)
    qc.measure(2, 2)
    qc
end

service = Service()
search_results = backend_search(service)
backend = least_busy(search_results)
@show backend.name
target = target_from_backend(backend, service)

qc = generate_bell_circuit()

transpiled_circuit, layout = transpile(qc, target)
@show transpiled_circuit.num_instructions

shots = 1024
job = run_sampler_job(service, backend, transpiled_circuit, shots)
samples = get_job_results(job, service)
@show samples
```

## License

Apache License 2.0
