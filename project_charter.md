# Project Charter
This charter is a living document, that will be refined as the project evolves, and as the dataset understanding, model perf, deployment constraints and business requirements become clearer.
## Business problem
All manufacturing processes have tolerances for errors or approximations, as planned by engineers during the design process. However, some manufactured items come with defects that are out of bound of tolerance values. These deviant items need to be detected quickly to ensure removal from production, as early as possible.
We need a way to identify theses defects reliably (superior to a given % we'll discuss later), accurately (we allow ourselves to have false positives rather than positive falses) and with a speed that matches production speed (eg a deviant item need to be spotted quickly enough so that sorting action can occur before the item is passed on another stage of the production process).
This project aims to give a solution to that problem.
## Users
- Production line operators
- Quality engineers
- Manufacturing supervisors
- Maintenance / automation team
- Data / AI team
- IT / infrastructure team
## Decisions supported
Decision : conformity (yes/no)
Recommandation : confidence (score)
## Success criteria
Will be refined during production test, but : 
- Target recall on defects: ≥ 99%
- Target false negative rate: ≤ 1%
- Target false positive rate: to be minimized and discussed with stakeholders
- Latency: compatible with production-line constraints
## Risks
All the typical risks for such a project:
- data leakage
- data domain out of scope for real data (this risk is under control with the dataset that'll be used for training)
- performance not aligned with production line requirements
all that could lead to an unusable model in prod : 
- too slow to act
- too many false positives (ultimately: time loss, confidence loss)
- too many false negatives (worst case scenario)
## MVP scope
Visual inspection with following features :
- can ingest item images
- detect defects or defects
- can aggregate results item / batch / line wise
- expose an inference API
- prepare a quality review interface
- can be deployed on edge in workshops
data set will be MVTec AD 2
