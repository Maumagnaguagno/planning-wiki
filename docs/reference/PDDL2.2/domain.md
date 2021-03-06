---
layout: default
title: PDDL 2.2 Domain
parent: PDDL 2.2
grand_parent: Reference
permalink: /ref/pddl22/domain
---
# Domain
{: .no_toc }

Contributors: {% git_author %}

The domain syntax for PDDL2.2 adds very minimal changes to the domain. As with any update to PDDL it introduces new requirements, however, other than that the only new syntax is Derived Predicates, which are defined in a similar way to how actions are defined, and are defined in the same section of the domain file.

```cl
(define
    (domain railways)
    (:requirements :derived-predicates :timed-initial-literals)
    (:types
        train station - object
    )
    (:predicates
        (train-not-in-use ?t - train)
        (train-has-guard ?t - train)
        (train-has-driver ?t - train)
        (train-usable ?t - train)
    )
    (:functions
        ... - omitted
    )
    (:durative-action MOVE-TRAIN
        ... - omitted
    )
    (:derived (train-usable ?t - train)
        (and
            (train-has-guard ?t)
            (train-has-driver ?t)
        )
    )
    (:derived
        ... - omitted
    )
)
```

## Contents
{: .no_toc .text-delta }

- TOC
{:toc }

## Requirements

[back to contents](#contents)

Support: Universal
{: .label .label-blue }
Usage: High
{: .label .label-green }

```cl
    (:requirements <requirement_name>)
```

Requirements are similar to import/include statements in programming languages, however as PDDL is a kind of declarative language, it is a `:requirement` as a given planner is "required" to facilitate some aspect of the language.

Multiple `:requirements` can be specified through a space separated list e.g.

```cl
    (:requirements :strips :adl :typing)
```

### List of Requirements
{: .no_toc }

This is a list of requirements that were added by PDDL2.2 to the language of PDDL.

- [:derived-predicates](./requirements#derived-predicates)
- [:timed-initial-literals](./requirements#timed-initial-literals)

## Derived Predicates

[back to contents](#contents)

Support: Medium
{: .label .label-yellow }
Usage: Low
{: .label .label-red }

```cl
    (:derived <predicate_name> <logical_expression>)
```

A derived predicate is declared by naming the predicate who's result is being derived, and a logical expression which is evaluated to work out the value.

Note, that a derived predicate is declared similarly to actions, in that we use the `:derived` keyword for each declaration of a derived predicate.

```cl
(:derived (train-usable ?t - train)
    (and
        (train-has-guard ?t)
        (train-has-driver ?t)
    )
)
```

The example above specifies that a train is only usable if it has a guard and a driver.
