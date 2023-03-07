# Organizations Support

* **Original Author(s):**: @hoegertn, @pflorek
* **Tracking Issue**: #{TRACKING_ISSUE}
* **API Bar Raiser**: @Naumel

The `aws-organizations` L2 construct library allows you to define your hierarchy
of organizational units and accounts. You can easily attach typed policies to your
organization resources. Additionally shared interfaces like `IAccount` helps
with the interop between different libraries, i.e. IAM alias or principal.

Managing these organization resources should have then the same developer
experience like any other resources in the AWS CDK.

## Working Backwards

> This section should contain one or more "artifacts from the future", as if the
> feature was already released and we are publishing its CHANGELOG, README,
> CONTRIBUTING.md and optionally a PRESS RELEASE. This is the most important
> section of your RFC. It's a powerful thought exercise which will challenge you
> to truly think about this feature from a user's point of view.
>
> Choose *one or more* of the options below:
>
> * **CHANGELOG**: Write the changelog entry for this feature in conventional
>   form (e.g. `feat(eks): cluster tags`). If this change includes a breaking
>   change, include a `BREAKING CHANGE` clause with information on how to
>   migrate. If migration is complicated, refer to a fictional GitHub issue and
>   add its contents here.
>
> * **README**: If this is a new feature, write the README section which
>   describes this new feature. It should describe the feature and walk users
>   through usage examples and description of the various options and behavior.
>
> * **PRESS RELEASE**: If this is a major feature (~6 months of work), write the
>   press release which announces this feature. The press release is a single
>   page that includes 7 paragraphs: (1) summary, (2) problem, (3) solution, (4)
>   leader quote, (5) user experience, (6) customer testimonial and (7) one
>   sentence call to action.

### Changelog

```
feat(organizations): Organizations L2
```

### README

___

# AWS Organizations Constructs Library

[AWS Organizations](https://aws.amazon.com/organizations/) provides you with the capability to centrally manage and govern
your cloud environment. You can manage and organize your accounts under a single bill, 
set central policies and configuration requirements for your entire organization, 
create custom permissions or capabilities within the organization, and delegate 
responsibilities to other accounts so they can manage on behalf of the organization.

This module is part of the [AWS Cloud Development Kit](https://github.com/aws/aws-cdk)
project. It allows you to manage your organization resources.

# Constructs

### Defining an organizational unit OU

In order to define your `OrganizationalUnit`, you must specify the name and the parent `OrganizationalUnit`.

```typescript
import * as organizations from '@aws-cdk/aws-organizations';

const root = organizations.OrganizationalUnit.fromAttributes({ organizationalUnitId: "r-examplerootid111" });
new organizations.OrganizationalUnit(this, "OrganizationalUnit", {
  organizationalUnitName: "MyFirstOrganizationalUnit",
  parent: root,
});
```

### Defining an account

In order to define your `Account`, you must specify the name and a unique account email. Optionally, you
may specify the parent organizational unit and the organizations role name.

```typescript
import * as organizations from '@aws-cdk/aws-organizations';

const ou = organizations.OrganizationalUnit.fromAttributes({
  organizationalUnitId: "ou-examplerootid111-exampleouid111"
});
new organizations.Account(this, "Account", {
  accountName: "MyFirstAccount",
  accountEmail: "any«example.com",
  parent: ou, // Defaults to the organiaztion root
  roleName: "OrganizationAccountAccessRole", // The default if don't specified
});
```

#### Using an account in other CDK modules

```typescript
interface IAccount {
  readonly accountId: number;
  readonly accountName: string;
}
```

### Defining policies

#### Defining a service control policy

#### Defining a backup policy

#### Defining a tag policy

#### Defining an AI opt-out policy

---

Ticking the box below indicates that the public API of this RFC has been
signed-off by the API bar raiser (the `api-approved` label was applied to the
RFC pull request):

```
[ ] Signed-off by API Bar Raiser @xxxxx
```

## Public FAQ

> This section should include answers to questions readers will likely ask about
> this release. Similar to the "working backwards", this section should be
> written in a language as if the feature is now released.
>
> The template includes a some common questions, feel free to add any questions
> that might be relevant to this feature or omit questions that you feel are not
> applicable.

### What are we launching today?

> What exactly are we launching? Is this a new feature in an existing module? A
> new module? A whole framework? A change in the CLI?

### Why should I use this feature?

> Describe use cases that are addressed by this feature.

## Internal FAQ

> The goal of this section is to help decide if this RFC should be implemented.
> It should include answers to questions that the team is likely ask. Contrary
> to the rest of the RFC, answers should be written "from the present" and
> likely discuss design approach, implementation plans, alternative considered
> and other considerations that will help decide if this RFC should be
> implemented.

### Why are we doing this?

> What is the motivation for this change?

### Why should we _not_ do this?

> Is there a way to address this use case with the current product? What are the
> downsides of implementing this feature?

### What is the technical solution (design) of this feature?

> Briefly describe the high-level design approach for implementing this feature.
>
> As appropriate, you can add an appendix with a more detailed design document.
>
> This is a good place to reference a prototype or proof of concept, which is
> highly recommended for most RFCs.

### Is this a breaking change?

> If the answer is no. Otherwise:
>
> Describe what ways did you consider to deliver this without breaking users?
>
> Make sure to include a `BREAKING CHANGE` clause under the CHANGELOG section with a description of the breaking
> changes and the migration path.

### What alternative solutions did you consider?

> Briefly describe alternative approaches that you considered. If there are
> hairy details, include them in an appendix.

### What are the drawbacks of this solution?

> Describe any problems/risks that can be introduced if we implement this RFC.

### What is the high-level project plan?

> Describe your plan on how to deliver this feature from prototyping to GA.
> Especially think about how to "bake" it in the open and get constant feedback
> from users before you stabilize the APIs.
>
> If you have a project board with your implementation plan, this is a good
> place to link to it.

### Are there any open issues that need to be addressed later?

> Describe any major open issues that this RFC did not take into account. Once
> the RFC is approved, create GitHub issues for these issues and update this RFC
> of the project board with these issue IDs.

## Appendix

Feel free to add any number of appendices as you see fit. Appendices are
expected to allow readers to dive deeper to certain sections if they like. For
example, you can include an appendix which describes the detailed design of an
algorithm and reference it from the FAQ.