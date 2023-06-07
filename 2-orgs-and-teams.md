## Organizations and Teams - Best Practices

### Scenario
One way to handle organizational segregation without losing collaboration would be to utilize different strategies for teams as described in [this GitHub blog posting](https://blog.github.com/2017-02-15-organize-your-experts-with-ad-hoc-teams/). For example, consider the following:

- We have a `Product Family` called **Mobile**
- Within the **Mobile** product family, we have multiple `Product Lines`
- Within each of the product lines, we have dozens of repositories
- We have teams that will work on multiple products across multiple product families
  - We want groupings of repositories according to their `Product Lines`, and we want groupings of the `Product Lines` in their respective `Product Families`
  - We want teams to see only the relevant repositories and not have to sift through thousands
  - We don't want to have to search for repositories to find them
  - We don't want to rely on the enforcement of `Tags`, as bad practices can easily break this organizational benefit

### Using `Orgs`
If we take the approach that we will utilize `Orgs` within GitHub to segregate our `Product Families` then we can certainly achieve the goal of limiting the overwhelming sea of repositories our developers will see when they login. This, however, presents us with a few challenges that will ultimately make the management of GitHub overwhelmingly difficult, and lead to a significant disconnect in software development and our SDLC workflow.

#### Challenges

- Settings, webhooks, permissions, teams and more, all have to be duplicated across _each_ organization and maintained. This will present a challenge if _anything_ is enforced across the company.
- Integrations with `CI/CD` platforms becomes manual and tedious to keep things integrated. One significant example is that a `Deploy Key` cannot be re-used, even in different organizations, which means that a Jenkins server might need dozens of keys, manually maintained, to integrate and automate workflows.
- Collaboration across teams, if they are in different organizations, becomes very limited and cumbersome, which promotes working in silos and not working together.
- Duplication of data and efforts becomes very prevalent, as users and teams will not have visibility into what other teams are developing. Even if they have _access_, they will not have _visibility_ or searchability across multiple organizations at once. This is costly for companies in time, effort and quality.

#### Benefits of having less organizations
We recommend always to start with the minimum number of organizations possible, and increase it if needed. Some reasons in favor of minimizing the number of organizations;
- Being able to leverage innersource using the search functionality in a single org (same as we do internally in GitHub)
- With teams (and nested teams) you can manage all the permissions with less administrative overhead
- Teams allow you to @ mention entire groups which helps to get notifications sorted out and notify the right people
- Permission strategy in a single org allows the team to configure policies that will be replicated for all the repositories and make that easier to manage
- Multiple organizations with multiple teams to manage can be useful for parts of the company that are productized or maintain an open source nature
- Automations (Github apps and OAuth apps) can be set on the organization level and help to keep secure policies across the org (or add default actions such us the all-employees read access)
- You can have an "all employees" team to promote openness
- You can create teams with expertises (data-science, javascript...). Use cc/ @mention to mention a group of people with experience on the matter
- Add topics to find the repositories within the organization
- Deploy Keys cannot be re-used between orgs. Use the deploy keys for deployments in your organization

Consider multiple organizations if;
- There is a full separation between two parts of the company, where one has one SSO and another has a different one. It's not allowed to have multiple configurations on SAML at the same time for 1 organization.
- Part of the company is 1+ products, with public-facing, open source contributions and multiple projects related
- If you have a full ecosystem around an internal product that makes sense to be completely separated from the rest (Github inside microsoft as an example)
- If a unified policy for the organization doesn't work and you want a completely different policy for another organization (with the risk of maintaining it as well). You need to be really careful with this reasoning as can be abused to create orgs.

#### Security recommendations
- Enable 2-factor authentication
- Enable SAML SSO to the organization
- Require SAML authentication to access the org content
- Do not allow people to change the visibility of the repos
- Set policies on the enterprise level so it applies to all possible organizations
- Add automations around security for the repositories (such as branch protection and permission mapping)

#### Additional resources
- [The GitHub guide to organizations](https://resources.github.com/downloads/github-guide-to-organizations.pdf)
- [Best Practices for Organizations](https://github.community/t5/Support-Protips/Best-Practices-for-Organizations/ba-p/10384)

### Using `Teams`
The concept of `Teams` in GitHub allows for greater flexibility for collaboration and integration, _as well as separation of repositories and **permissions**_. With _nested teams_ we can create a hierarchy for our applications, create communities of practice, invoke logical groupings of functional areas, as well as manage our teams of people effectively. If we take a step back and look at `Teams` as being more than simply HR groupings of people we can see many ways to effectively organize our software.

#### Uses for `Teams`
- Teams can be used to logically separate `Product Families`
- Teams can be used to logically separate `Products`
- Teams can be used to logically correlate areas of expertise
- Teams can be used to logically correlate `Product Features`
- Teams can be used to logically group areas of responsibility
- Teams can be nested, which provides logical groupings for these teams' areas of ownership

#### Product and People teams

![team-org](https://user-images.githubusercontent.com/865381/37910942-c2c8c012-30dc-11e8-910b-1bda5b22fb25.png)

We have a `Product Family Team` underneath that Org. Within that `Product Family Team`, we can have multiple `Product Teams`. We want to make sure that people working on `Product A` are able to see only the repositories belonging to it.

If we have all 3 `Products` (`Product-A`, `Product-B` and `Product-C`) created as `Teams`, and have each of these `Teams` as a children of the `Product Family Team`, then we can see all repos from the `Product Family` or just the repos belonging to the `Product` in the teams view (`https://github.com/orgs/:org/teams/:teamName/repositories`). We can then add these teams to the repositories for them to get access.

Once we have logically organized our `Product Family` and `Product Teams`, we can organize our developers with `People Teams`, and add those `People Teams` into the repositories as necessary. In the image, some people from `devGroupA` also belong to `org/SQL` and `org/security` and each of those groups can be added to repositories as needed to provide the right access.

Another example: In the image below, we see that we have `Client Apps` as the `Product Family` and Atom as the `Product`. The only repositories visible from this team's view are those that belong to the Atom product team.

![github-teams-8](https://user-images.githubusercontent.com/865381/36806811-3c0eee04-1c8f-11e8-8088-a7c57d3fe006.png)
 
#### How to configure the structure
-  Plan the `Product families` and `Product teams` that you want to have
-  Plan the `Developer teams` that you want to have
-  You can go to https://github.com/orgs/:org/teams and:
  - Create the `Product families`
  - Create the `Product teams` and assign their parent as the corresponding `Product family`
  - Add the `Product teams` access to the repositories they need to have access to
  - Create an `Everyone team`. This team is useful for wide company announcements without hosting a webinar to explain something. Try not to abuse this `@all` pings.
  - Create the `People teams` and assign `Everyone team` as the parent
  - Add the `People teams` to the repositories as needed
	
> ⚠️ To add teams as children of other teams they cannot be secret teams.

#### Team interests
Additionally you can create teams for interests/technology in order to help with PR review processes or issue discussions (javascript, go, data science...). People can join these teams through their own interest to help on certain projects if their support is needed.

Creating a process within the company to create new `team interests` teams is recommended.

#### Team sync enablement
If you use a SAML provider that supports [team synchronization](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/synchronizing-teams-between-your-identity-provider-and-github), you may want to enable it for the `People teams` and not for the `Product` teams. Team sync can only be enabled on leafs (groups with no children teams), so people teams are the best option.

You can make the `People` teams structure match your SAML provider structure if needed and then create the parents as logical structures.

#### Additional resources
- [Organize your experts with ad hoc teams](https://github.blog/2017-02-15-organize-your-experts-with-ad-hoc-teams/)