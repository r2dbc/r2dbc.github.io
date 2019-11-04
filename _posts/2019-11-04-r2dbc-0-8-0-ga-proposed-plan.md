---
layout: post
title:  "R2DBC 0.8.0 GA proposed plan"
date:   2019-11-04 11:00:00 -0500
tags: [schedule, minutes]
author: Mark Paluch
---

After almost two years in development, we're reaching a stage where we feel confident enough about R2DBC being ready for a generally available release.
Thanks to everyone involved for all contributions, hard work, and numerous hours of discussion that enabled the R2DBC endeavor reaching this stage.

# SPI Changes

We have a few things left before we can ship the actual release. As per [our monthly call](https://groups.google.com/forum/#!topic/r2dbc/72yGm7CXZf4), we will merge the last remaining SPI changes during this week. Once merged, the SPI should be considered in the state that is going to be released.

# BOM Changes

We plan to include open source, community-maintained R2DBC drivers in the R2DBC BOM for users to easier consume R2DBC. The first release of the BOM will require a bit of coordination as we intend to release the BOM shortly after releasing R2DBC SPI. This coordination should be a one-time effort. Subsequent BOM releases should be considered an opportunity to carry driver upgrades in a service release mode. We aim for regular (e.g. monthly or another regular release interval) releases, so changes in drivers reach consumers quickly that decide for a dependency-managed arrangement. 

The BOM is by no means an obligation nor a requirement to ship changes. If a driver is available in a newer version from Maven Central, then the BOM can be seen as an arrangement to simplify dependency upgrades to consumers of R2DBC artifacts. If you're maintaining an R2DBC driver and want to get included in the BOM, please [submit a pull request](https://github.com/r2dbc/r2dbc-bom).

Going forward, we plan to keep R2DBC SPI 0.8.x binary compatible and postpone changes that require behavioral or additional API to the upcoming 0.9 line.

# Release Schedule

We want to propose the following schedule:

1. Release of R2DBC SPI 0.8.0.RELEASE and the TCK on Monday, Nov 25 to Maven Central
2. Use the week of Nov 25 to 28 to release all drivers that want to participate in the 0.8 Release Train to Maven Central
3. Release the R2DBC BOM Arabba-RELEASE on Nov 29 as the last component to Maven Central
4. Announce R2DBC 0.8 GA on Dec 2nd

Cheers, 
Mark