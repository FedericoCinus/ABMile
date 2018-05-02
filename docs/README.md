# ABMile
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
## ToC
- [Overview](#overview)
- [Run](#run)
- [Solution](#Solution)
- [Results](#Results)


## Overview

In this work is introduced the Last Mile problem and the Agent-Based modelling process. A solution for the Last Mile problem is proposed suggesting an active engagement of the population. Some estimation has been done in order to make the simulation suitable for representing the city of Turin and actual cost of the delivering process. Results show the robustness of the proposed solution both in economical and user’s engagement terms, discussing also extreme situation.

More detail on Article.pdf in the Github repository.

## Run

Download ABMile from GitHub repository.
Code is written in NetLogo 6.0 and it is possible to freely download it and run the simulation (#https://ccl.northwestern.edu/netlogo/download.shtml).

To run open `ABMile` and click on `Setup` and then `Go`. Choose parameters before running.

![gif][gif]

## Solution

Delivery is carry out by Users. These are agents created in random patches and with and assigned random patches as destination. A special patchset is created to represent the storages around the city. Each packages is placed in a locker-patch ad assigned a random point on the map as destination. The User will go from his position to the position of the package, then go the destination of the package and lastly to his own destination.

To optimize the travel we will use an auction for each package. Moreover packages are not placed randomly in the storages patches but, if the space is enough, each package will be placed in the storage nearest to its destination.


## Results

Using genetic algorithms implemented in Behavior Search 6.0 we optimized the num- ber of storages and their space, keeping all other estimated parameters fixed such as the number of users, the number of packs and the cost of each box in the storage.

Figure below show the fitness minimization (expenses) with the following parameters: 1400 packs, 700 users, 1e/km for users’ deviation, 1.75e as maximum expense for a pack delivery, 0.2e cost storage’s box.

![gen][gen]

Considering 0.8e as storage’s box cost, we find again that the number of boxes in each storage is greater than the minimum needed. This implies that spending money for having bigger storage is useful in case a pack has to be delivered in the neighborhood.

![gen2][gen2]

May be found interesting for the reader to have a deeper look at two of the most important curves in our simulation: number packs vs. time and total expenses vs. time. The figure below show that the number of packs exponentially decreases with time as expected. On the other hand the total expenses approximately increase as a logarithm, which compensates the number of packs trend.

![concl][concl]

[gen]: img/gen.png "Behavior Search result: 10 storages with 304 boxes each, total expense 1439.28"
[gen2]: img/gen2.png "Behavior Search result: 10 storages with 153 boxes each, total expense 1542.02"
[concl]: img/concl.png
[gif]: img/gif.gif "gif"
