# Django Features

## TODOs

- Write up overview in English
- Move the mermaid chart to the proper location
- Write up descriptions of each phase
- Write up instructions for SC / Feature Review team for each phase
- Generate URLs for various queues for people to bookmark
- Write up instructions for an expedited DEP process

## Have an idea for Django?

Please know, things in Django take a while. You will need to be patient.

Please start with reviewing the [new feature process in Django](#djangos-new-feature-process).

Next, go [create an issue in this repository](https://github.com/tim-schilling/new-features/issues/new).

## Want to help steer Django?

There are three queues that need community involvement:

- [Is there community support?](https://github.com/tim-schilling/new-features/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22phase%20%2F%20is%20there%20community%20support%22)
    - Review the open tickets in this queue. Please share support on this via emojis.
    - Please follow the [Emoji Reaction guide](#emoji-reaction-guide)
    - See [Is there community support?](#is-there-community-support) for more details
- [Is a feature expected in Django core?](https://github.com/tim-schilling/new-features/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22phase%20%2F%20is%20this%20expected%20in%20core%22)
    - Weigh-in on whether a feature should exist in Django core
    - See [Is this expected in Django?](#is-this-expected-in-django) for more details
- [Needing volunteers to implement or implementation review](https://github.com/tim-schilling/new-features/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22phase%20%2F%20needs%20community%20DEP%22)
    - Help implement or design features
    - See [Can we do it?](#can-we-do-it) for more details

### Leaving comments

The community is encouraged to engage in discussion about a feature idea. Please try to
avoid one-on-one discussions here though when possible. Long threads are difficult to
follow and require a person to summarize periodically.

### Things not to do

Please avoid doing the following:

- Writing comments that are "+1" or "-1". Use emojis to share those opinions, please.
- Writing comments that are "What's the state of this?" You can see which phase of the process the idea is in by looking at the labels


## Django's new feature process

This repository is used to contain Django's new feature process. The
purpose is to identify features that the community deems helpful and
necessary to exist within Django.

The high level flow of the process can be seen in the chart below:

```mermaid
flowchart TD
    newIdea[New Idea]@{ shape: circle} --> isGood{Is there community support?}
    isGood -->|No| wontfix[Won't Fix]
    isGood -->|Yes|featureType{Is this expected in Django?}
    featureType --> |No|delightful{Can it be a 3rd party package?}
    featureType --> |Yes|scDEP[SC drafts DEP]
    scDEP --> expected{Can we do it?}
    expected --> |Yes|scDEPFinish[Implementor finishes DEP]
    expected --> |wait for resources| expected
    scDEPFinish --> tracCreated[Create Trac ticket / Implement]
    delightful --> |Yes|package[Create a package]@{ shape: dbl-circ}
    delightful --> |No|authorDEP[Author creates DEP]
    authorDEP --> |Rejected|wontfix@{ shape: dbl-circ}
    authorDEP --> |Approved|tracCreated@{ shape: dbl-circ}
```

### Is there community support?

The initial phase of every feature is understanding if there's community
support for an idea. Community members should express their opinion in
two ways:

- An emoji reaction for simple opinions
- A written comment for detailed support or criticism

#### Emoji reaction guide

Using the following emojis on an issue has the related meaning.

- 👍 This is something I would use
- 👎 This is something that would cause problems for me or Django
- 😕 I’m indifferent to this
- 🎉 This is an easy win

#### Raising awareness

If you've created a feature request and want to bring more attention to it,
you should consider some of the following:

- Post about it on Social Media with the #Django hashtag
- Post about it on the [Django Forum](https://forum.djangoproject.com/)
- Write a blog post
- Create a video
- Give a conference talk

The larger your idea, the more investment you may need to make to convince
the community to support it.

#### How is community support determined?

The [Steering Council](https://docs.djangoproject.com/en/dev/internals/organization/#steering-council)
will review issues periodically. They will review
a subset of issues in this category and determine whether there's community
support for an idea. This is to the Steering Council's discretion.

### Is this expected in Django?

The phase after there's community support is the phase to determine if the
feature idea is expected in Django core. Community members are encouraged to
voice their opinion on why something is or is not expected in Django.

#### How are features determined to be within Django?

The Steering Council will review issues periodically. They will review a
subset of issues in this category and weigh the perspectives of the
community and determine whether a feature should be added to Django.
This is to the Steering Council's discretion.

### Can we do it?

The phase after it's agreed upon that the feature belongs in Django is
determining whether the feature can be implemented. Advancing beyond this
phase requires a [DEP](https://github.com/django/deps/) to be created.
The [Steering Council](https://docs.djangoproject.com/en/dev/internals/organization/#steering-council) or a community
member can create the first draft. It should contain everything but the
technical details of implementation (unless those are known already).
The community needs a person or a group of people to volunteer to implement
the feature.

For smaller issues, several steps of the DEP process can be skipped as
they will already have occurred.

For larger issues, the DEP process should be followed, more closely.
This is because the actual implementation of the feature will need
to be agreed upon before any code can be merged.

#### How do we determine if we can do it?

When there is a DEP that the Steering Council is in agreement upon which
has everything but perhaps the last of the technical details, a Trac
ticket can be created and implementation Pull Requests to Django can
be sent.

This does not mean work can't start beforehand, but we shouldn't ask for
Fellow's involvement until these things are completed.


### Can the feature be a third-party package?

The phase when it's determined that a feature has community support, but
shouldn't be in Django core is determining whether the feature should be a
third-party package. Most features should strive to be third-party packages.
This approach allows for faster iteration and more variability in our
ecosystem. 

It's possible that a feature can't be a third-party package due to the nature
of the feature or limitations of Django. In this case, the DEP process should
be followed. This [DEP](https://github.com/django/deps/) must be written by
a community member rather than the [Steering Council](https://docs.djangoproject.com/en/dev/internals/organization/#steering-council).

## Do you have feedback about the process?

Please share your opinions on the [Forum](https://forum.djangoproject.com/c/internals/5).


