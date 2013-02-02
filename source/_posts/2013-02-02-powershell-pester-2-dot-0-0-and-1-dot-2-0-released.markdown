---
layout: post
title: "PowerShell Pester 2.0.0 and 1.2.0 Released"
date: 2013-02-02 15:34
comments: true
categories:
---
After a whirlwind of activity on the [Pester](https://github.com/pester/Pester) codebase I'm happy to announce the latest release of Pester. Versions 1.2.0 and 2.0.0 are identical feature wise except for one subtle difference that I'll get into soon.

## New Assertion/Expectation Syntax

In prior versions of Pester, we have the dot notation assertion syntax.

```powershell
$some_string.should.be("some value")
```

This required some [clever and downright nasty hacks](https://github.com/pester/Pester/blob/bf3afbf330808cfee8a26665a77c9388ae432286/ObjectAdaptations/types.ps1xml) to the PowerShell runtime. This created a [few](https://github.com/pester/Pester/issues/19) [issues](https://github.com/pester/Pester/issues/27) for some users and I wanted to get that fixed. It turned out the extension on Object was the root issue so I investigated a pipeline based assertion syntax. Here is the result:

```powershell
$deployDir | Should Be "C:\inetpub\wwwroot\myApp"
"iis:\Sites\myApp" | Should Exist
"C:\test\rush_albums.txt" | Should Contain 2112
"" | Should Be NullOrEmpty
{ throw } | Should Throw
```

Negative statements work too:

```powershell
2 | Should Not Be 1
"C:\temp\deployment_scratch_space" | Should Not Exist
"C:\test\rush_albums.txt" | Should Not Contain 5150
1,2,3 | Should Not Be NullOrEmpty
{ Deploy-Website "superawesome" } | Should Not Throw
```

Extending the syntax is simply a matter of adding domain specific expectations, that follow the Pester function naming
conventions, to your test suite:

```powershell
function PesterBeCanadian($sentence) {
    return ($sentence -match ".*[,\ ]eh.$")
}

function PesterBeCanadianFailureMessage($sentence) {
    return "Expected: {$sentence} to end with 'eh'"
}

function NotPesterBeCanadianFailureMessage($sentence) {
    return "Expected: {$sentence} ended with eh, you hoser!"
}
```

Simply source that code in your tests and you can write the following:

```powershell
Describe "a few sentences" {
    Context "when scott says something" {
        It "is Canadian" {
            $what_scott_says = "Good show, eh?" 
            $what_scott_says | Should BeCanadian
        }
    }

    Context "when pete hodgson says something" {
        It "is not Canadian" {
            $what_pete_says = "Have you tried testing it with Frank?"
            $what_pete_says | Should Not BeCanadian
        }
    }
}
```

Pretty cool, eh? I feel that this can lessen the potential bloat of expectations in Pester and allow people to write
test suites that fit their infrastructure domain model. The exepectations are also very [easy to test](https://github.com/pester/Pester/blob/master/Functions/Assertions/Be.Tests.ps1) in isolation

## Mocks!

This was released earlier but I didn't really announce anything. Thanks to [Matt Wrock](http://www.mattwrock.com/)([twitter](https://twitter.com/mwrockx)) Pester has the ability to mock cmdlets. I'm looking forward to trying this out on my next project.

```powershell
Mock Get-Location { return "you are home, sir." }
Get-Location | Should Be "you are home, sir."
```

## Description Tagging

Thanks to [Rich Siegel](https://github.com/rismoney), Pester can now run blocks that fit a certain tag.

```powershell
Describe -Tag "Acceptance" "Website deployment flow" {

    ...

}

# and run it like this:
Invoke-Pester -Tag Acceptance
```

## Xml Reporting

Another contributor is [Max Bergmann](https://github.com/mbergmann) who added NUnit style xml reporting to Pester runs.
We are even using it in Pester's own [CI
build](http://teamcity.codebetter.com/project.html?projectId=project261&tab=projectOverview)

## Why 1.2.0 and 2.0.0?

The motivation for this release is to fix the issues people have add where a `should` property is added to every Object.
I'm not sure how exactly it was breaking things, but it was messing anyways, and I wanted to get rid of it.

In version `1.2.0`, you can disable the old assertions by running Pester with the `-DisableOldStyleAssertions`. This will
mean that your test suite has to only use the new pipeline style expectations.

```powershell
# version 1.2.0 has this switch
Invoke-Pester -DisableOldStyleAssertions
```

For version `2.0.0` we disable the old style assertions and you need to explicitly enable them using the
`-EnableLegacyAssertions` switch. In the next significant release we're going to remove the dot style assertions
completely from the codebase.

```powershell
# version 2.0.0 has this switch
Invoke-Pester -EnableLegacyAssertions
```

So if you're upgrading Pester, then you should probably move to `1.2.0` first. If you can run your tests with the
`-DisableOldStyleAssertions` flag set, then you should be fine to move to `2.0.0`. If you're starting from scratch, then
definitely use `2.0.0`.

## What's Left To Do?

Lots and lots of documenting. The `Get-Help` pages need to be updated and I want to get pesterbdd.com up as soon as
possible. I think version 2 should be a fairly stable version of Pester.

If you're interested in contributing to Pester please joing the [google group](https://groups.google.com/forum/?fromgroups#!forum/pester).


