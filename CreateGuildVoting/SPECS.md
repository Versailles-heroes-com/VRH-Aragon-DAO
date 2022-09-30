## Voting fork SPECS

Allow creating a new vote only when user has at least `minGuildBalance` and 
at least `minTime` has passed between user's last vote and time now when they want to create a new vote
    
*   Min guild balance
    Should allow a token holder to create a new Aragon Vote 
    given that the token holder has the required `minGuildBalance` voting power
    
    The voting power of a token holder is calculated by `tokens locked` * `lock time`
    as specified in [Versailles DAO Paper](https://github.com/Versailles-heroes-com/versailles-heroes-DAO/blob/main/README.md)
* Min time
    Should allow a token holder to create a new vote only if there is at least `minTime` passed between their last vote and time now when they want to create a new vote

To prevent DAO to set unrealistic limits for `minGuildBalance` and `minTime`, `minGuildBalance` is required to be the equivalent of at least `10000` tokens locked for `one year` (1e18 precision) (which equals to `2500000000000000000000`)
and `minTime` is required to be between half a day and 2 weeks

Changing votes is not allowed.

To incentivize people to vote early and not wait and see what's the outcome of the vote and vote near the end of vote,
the voting power they had for the snapshot of for that vote is getting smaller proportional to the time left for that vote(with a cutoff period of `voteTime` / 2 between creation of vote and when decrease starts to happen)

Voting app will have `CREATE_VOTES_ROLE` permissions set to anyone(`0xffffffffffffffffffffffffffffffffffffffff`) because the balance check will be done inside the Voting app and not through a forwarder