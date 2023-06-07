## Organization archetypes

The intention of this document is to provide some guidance and suggestions to customers who are wondering how they should structure organizations and teams in their GitHub Enterprise environment. The idea isn't to give hard and fast rules on which approach is better than the other, but to give examples of when one approach might be preferable to another depending on the use case.

#### 1. A single organization with direct organization membership for repository access (not teams)
              ________________
              |     Org      |
              |    ______    |
              |   |      |\  |
              |   | Repo | \ |
              |   |______|  \|
              |              |
              |    ______    |\
              |   |      |   | \
              |   | Repo |---|-- All users
              |   |______|   |/
              |              |
              |    ______   /|
              |   |      | / |
              |   | Repo |/  |
              |   |______|   |
              |              |
              |______________|

Summary: In this case there would be a single organization on the GitHub Enterprise environment to which all users belong. All users [added to the organization](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-organizations-and-teams/inviting-users-to-join-your-organization) are granted write access by [setting the organization base permission to "Write"](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-organizations-and-teams/setting-base-permissions-for-an-organization). In this case teams are used to organize users, not for granting them access to repositories.

Scenarios where this makes sense:
- Works best in small companies
  - where everyone works on everything (so they all need the same access to all repos)
  - startup model
  - high trust
- Can work in medium sized companies as well
  - where trust is high

Scenarios where this doesn't make sense:
- Companies with siloed business divisions
- Companies with strict security constraints

Benefit:
- All members and teams can be @mentioned to get their input on all projects
- Faciliates InnerSource projects

Drawback:
- Loose organization

Note: This is pretty much how GitHub operates although technically everyone has access to all repositories because we are in ```@github/employees```.

Examples: GitHub

#### 2. A single organization with multiple teams to manage repository access

                    ________________
                    |     Org      |
                    |    ______    |
                    |   |      |\  |
        Team A------|---| Repo | \ |
                    |   |______|  \|
                    |              |
                    |    ______    |\
                    |   |      |   | \
                    |   | Repo |---|-- Team B
                    |   |______|   |
                    |              |
                    |    ______    |
                    |   |      |   |
        Team C------|---| Repo |   |
                    |   |______|   |
                    |              |
                    |______________|

Summary: Similar to the scenario above, except that teams are used to control repository access with more granularity.

Scenarios where this makes sense:
- Works in small companies with strict development roles, or lower trust
- Medium sized companies

Scenarios where this doesn't make sense:
- Small startups: administrating teams may take more time that it is worth in a 10 or 20 seat company where everyone works on, or at least is aware of, everything
- Large companies where no single owner should have access to all repositories

Benefit:
- All teams are able to @mention each other since they are in the same organization
- Faciliates InnerSource projects and collaboration across business units

Drawback:
- Can become unwieldy at a company with many teams at a large scale

#### 3. Multiple organizations divided per business unit with direct organization membership

                      ________________         ________________    
                      |     Org      |         |     Org      |
                      |    ______    |         |    ______    |
                      |   |      |   |         |   |      |   |
                      |   | Repo |   |         |   | Repo |   |
                      |   |______|   |         |   |______|   |
                      |              |         |              |
      Business        |    ______    |         |    ______    |       Business
       Unit A  -----  |   |      |   |         |   |      |   | ------ Unit B
                      |   | Repo |   |         |   | Repo |   |
                      |   |______|   |         |   |______|   |
                      |              |         |              |
                      |    ______    |         |    ______    |
                      |   |      |   |         |   |      |   |
                      |   | Repo |   |         |   | Repo |   |
                      |   |______|   |         |   |______|   |
                      |              |         |              |
                      |______________|         |______________|

Summary: In this scenario organizations map to business units, products, or some other silo and are largely separate. Similar to the first scenario, all users have write access to organizational repositories [granted by the organization base permission](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-organizations-and-teams/setting-base-permissions-for-an-organization). Some users may be members of multiple organizations. Over time organizations may merge together and access via teams may be required.

Scenarios where this makes sense:
- Works well when there are many repositories per business unit
- Works very well if there are strict access policies and for larger companies
- Work in companies that are large enough to have groups that don't need to work together
- Works well in companies with requirements for segregation of duties and access restrictions
- Large companies where no single owner should have access to all repositories

Scenarios where this may not make sense:
- If contribution across business units is important
- If there is a need to @mention teams from different organizations

Benefit:
- Manage access without team administration

Drawback:
- May hinder collaboration or happenstance of developers discovering projects they are interested in
- Reduces searchability of resources within the company


#### 4. Multiple organizations with multiple teams to manage repository access 

                ________________            ________________    
                |     Org      |            |     Org      |
                |    ______    |            |    ______    |
                |   |      |\  |            |   |      |   |
    Team A------|   | Repo | \ |            |   | Repo |   |------Team D
                |   |______|  \|            |   |______|   |
                |              |            |              |
                |    ______    |\           |    ______    |
                |   |      |   | \          |   |      |   |
                |   | Repo |---|--Team B    |   | Repo |---|--Team E
                |   |______|   | /          |   |______|   | /
                |              |/           |              |/
                |    ______    |            |    ______    |
                |   |      |  /|            |   |      |  /|
    Team C------|   | Repo | / |            |   | Repo | / |
                |   |______|/  |            |   |______|/  |
                |              |            |              |
                |______________|            |______________|

Summary: This is similar to the second scenario but at a larger scale, in large companies that have multiple, large business units that each need a granular level of control over repository access.  

Scenarios where this makes sense:
- Works well there are many repositories per business unit
- Works very well if there are strict access policies and for larger companies
- Work in companies that are large enough to have groups that don't need to work together
- Works well in companies with requirements for segregation of duties and access restrictions
- Large companies where no single owner should have access to all repositories

Scenarios where this may not make sense:
- If contribution across business units is important
- If there is a need to @mention teams from a different organization

Benefit:
- High level of separation and access control required in large companies

Drawback:
- May hinder collaboration or happenstance of developers discovering projects they are interested in
- Reduces searchability of resources within the company