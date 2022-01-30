# Solidity DevSecOps Standard.

DevSecOps standard for teams wishing to build secure software for EVM-based blockchain networks from the ground up and post deployment.
A more detailed guide is in development. This checklist itself is still being improved upon.

_Based on work by [ConsenSys Diligence](https://consensys.github.io/smart-contract-best-practices/), [the Secureum](https://secureum.xyz/) and inspired by the [solcurity standard](https://github.com/Rari-Capital/solcurity)._

### Human Elements

- Educate developers on security best practices i.e [ConsenSys](https://consensys.github.io/smart-contract-best-practices/) and [Trail of Bits](https://github.com/crytic/building-secure-contracts)
- Have atleast one security engineer monitoring and reviewing commits for security pitfalls and potential vulnerabilities whether internally or contracted.

### Code

- Your code must be well tested with ideally 100% code coverage.
- Adhere to a standard programming style to improve readability and auditability i.e the official [solidity style](https://docs.soliditylang.org/en/v0.8.11/style-guide.html). 
- Keep it clean i.e
- Write [Scribble](https://consensys.net/diligence/scribble/) properties for robust and incremental fuzzing with MythX(Harvey) or Echidna upon commits.
- Code should be written according to the following principles and standards starting with [Saltzer and Shroeder's 10 secure design principles](https://github.com/morphean-sec/secure-smart-contract-design-principles) as applied to smart contracts.

### CI/CD Pipeline

- Integrate Slither and Echidna into GitHub Actions. Alternatively, use the paid SaaS security tools MythX and Diligence Fuzzing.

### Pre-audit

-

### Post deployment to mainnet

- Integrate a security event alert system like Tenderly to alert you to suspicious events.
