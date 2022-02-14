# Solidity DevSecOps Standard.

DevSecOps standard for teams wishing to build secure software for EVM-based blockchain networks from the ground up and post deployment.
A more detailed guide is in development. This checklist itself is still being improved upon.

_Based on work by [ConsenSys Diligence](https://consensys.github.io/smart-contract-best-practices/), [the Secureum](https://secureum.xyz/) and inspired by the [solcurity standard](https://github.com/Rari-Capital/solcurity)._

### Human Elements/Mindset

- Educate developers on security best practices i.e [ConsenSys](https://consensys.github.io/smart-contract-best-practices/) and [Trail of Bits](https://github.com/crytic/building-secure-contracts)
- Have atleast one security engineer monitoring and reviewing commits for security pitfalls and potential vulnerabilities whether internally or contracted. If you absolutely cannot afford one then atleast have a security oriented developer on the team reviewing git commits with the [Solcurity Standard](https://github.com/Rari-Capital/solcurity).
- Code should be written according to the following principles and standards starting with [Saltzer and Shroeder's 10 secure design principles](https://github.com/morphean-sec/secure-smart-contract-design-principles) as applied to smart contracts.

### Code

- Find access control issues or other problems in your code with [Solgrep](https://github.com/tintinweb/solgrep) - A scriptable semantic grep utility for solidity
- Your code must be well tested(unit and integration) with ideally 100% code coverage. **Important**: Your README should give clear instructions for running the test suite. If any dependencies are not packaged with your code (e.g. Truffle), list them and their exact versions.
- Adhere to a standard programming style to improve readability and auditability i.e the official [solidity style](https://docs.soliditylang.org/en/v0.8.11/style-guide.html). 
- Use well tested libraries like [OpenZeppelin libraries](https://docs.openzeppelin.com/contracts/4.x/) to implement functions i.e "Don't roll your own cryptography" or "Don't reinvent the wheel." to minimize bugs and mistakes that may lead to disasters.
- Keep it clean i.e
1. Run a linter on your code. Fix any errors or warnings unless you have a good reason not to. For Solidity, we like Ethlint.
2. If the compiler outputs any warnings, address them.
3. Remove any comments that indicate unfinished work (ie. TODO or FIXME). (This is assuming it’s your final audit before deploying to mainnet. If not, exercise your judgement about what makes sense to leave in.)
4. Remove any code that has been commented out.
5. Remove any code you don’t need.
- Write [Scribble](https://consensys.net/diligence/scribble/) properties for robust and incremental fuzzing with MythX(Harvey) or Echidna upon commits. An introduction to fuzzing Ethereum smart contracts with Echidna from ToB itself can be found [here](https://github.com/crytic/building-secure-contracts/tree/master/program-analysis/echidna).
- Ensure your code has proper audit logs and event emissions set up. Effective alerting could mean the difference between being rekt and staying afloat.
- Consider importing and using the [Pausable library](https://docs.openzeppelin.com/contracts/4.x/api/security#Pausable) from OpenZeppelin as a multi-sig function(or centralized onlyOwner) in order to freeze the contract in case of an exploit.

### CI/CD Pipeline

- Integrate [Slither](https://github.com/crytic/slither-action) and [Echidna](https://github.com/crytic/echidna-action) into GitHub Actions. Alternatively, use the paid SaaS security tools [MythX](https://mythx.io/) and [Diligence Fuzzing](https://consensys.net/diligence/fuzzing/) or use the integrated Foundry and DappTools fuzzers and formal verification tools. However, it is strongly suggested to write your property tests with [Scribble](https://consensys.net/diligence/scribble/). A specification language from ConsenSys Diligence that takes your fuzzing and testing to a whole new level.
1. MythX recommended usage:
- Quick scan every commit.
- Standard scan at development milestones.
- Deep scan prior to audits/releases.

Diligence Fuzzing and Echidna fuzzing should be done as often as possible to reduce security debt upon audits.

### Post deployment to mainnet

- Integrate a security event alert system like [Tenderly](https://tenderly.co/) to alert you to suspicious events.
- Acquire insurance in case of exploits. An example of a project offering exploit insurance is [Fides](https://confidencesystem.webflow.io/).
- Set up a bug bounty programme for responsible disclosure via platforms like Fides and [Immunefi](https://immunefi.com/)
- Make sure your development/security team is easily accessible in case a security researcher wishes to alert you to a problem in your code. Establish points of contact i.e e-mail addresses, Telegram/Twitter usernames(with open DMs) etc in your project's README, website and via [Blockchain Security Contacts](https://github.com/crytic/blockchain-security-contacts)
- The security of the privileged wallets should be of the utmost importance and each of the holders(if using hardware wallets) MUST read and follow these [best practices](https://blog.trailofbits.com/2018/11/27/10-rules-for-the-secure-use-of-cryptocurrency-hardware-wallets/) without fail.
- Ensure you have an incident response plan and assume that your smart contracts can and will be compromised. The code might be free of obvious bugs but an attacker might take over the contract owner's keys.
