# Tokenomics

## Scope
Token supply design, incentive structures, and game-theoretic mechanics that motivate network participants.

## Core principles
- Incentive alignment is key: if token holders and users benefit from the network growing, the network has a chance; if incentives are misaligned, governance gridlock or rug pulls follow.
- Inflation (minting new tokens) funds protocol development and validator rewards; deflation (burning tokens) increases scarcity and can signal value capture.
- Vesting schedules (team tokens locked, released over years) reduce dumping and align incentives with long-term success.
- Token sinks (burning, staking for fees, buyback mechanisms) reduce supply; if burn rate exceeds mint rate, tokens become deflationary and scarcer.
- Governance tokens grant voting rights to token holders; voting power concentration (whale dominance) leads to decisions favoring large holders at the expense of small stakeholders.

## Apex practices
- Model incentives with game theory: does a rational actor want to hold, stake, sell, or attack? If all actions align with protocol health, incentives are sound.
- Use transparent tokenomics: document supply schedule, vesting, emission rates, and burn mechanisms so users understand dilution risk.
- Time-lock governance changes (48-72 hour delays) give users time to exit if they disagree with a proposal.
- Reward protocol treasury (not just validators/miners) so governance can invest in R&D and community.

## Pitfalls
- Hyperinflation (unlimited supply, no caps) erodes token value and incentivizes immediate exit; Bitcoin's 21M cap is valuable precisely because it's fixed and known.
- Governance attacks (51% attack on voting, bribe attacks where an attacker bribes token holders to vote for unfavorable changes).
- Token lockup and vesting not enforced; early investors and team can dump tokens, tanking the price and destroying incentives.

## Tools & references
Vitalik's "Cryptoeconomics" writings, TokenTerminal (tokenomics analytics), Messari (token analysis), game theory frameworks (incentive compatibility, mechanism design), supply schedules (Bitcoin, Ethereum), staking rewards (Lido, Cosmos).
