# Wipefest Event Configurations

## Where are we?

When [Wipefest](https://www.wipefest.net/) constructs the events view, it:

* Loads the relevant configurations from this repository
* Builds a [Warcraft Logs](https://www.warcraftlogs.com/) filter based on these configurations
* Queries the [Warcraft Logs API](https://www.warcraftlogs.com/v1/docs) using this filter
* Using the same configurations, decides how to convert the returned Warcraft Logs events into Wipefest events
* Renders these events

## What does it mean?

*Pending: annotated examples and documentation.*

## How can I contribute?

All of the configuration is contained in JSON files,
which makes it very easy for people to contribute
without necessarily needing any extensive programming know-how.

The following workflow aims to guide you through the process of making a change
(all of it can be done right here in your browser -
no complicated development setup required)!

*Some finer details about typical pull request workflows can be found [here](https://gist.github.com/Chaser324/ce0505fbed06b947d962).*

#### 1. Find or create an issue to work on.

[Issues can be found here](https://github.com/JoshYaxley/Wipefest.EventConfigs/issues).
If you want to create an issue,
it might be worth discussing it on [our Discord server](https://discord.gg/QhE4hfS) first,
to work out any details and just make sure that it's needed.

For this example, we will solve [this issue](https://github.com/JoshYaxley/Wipefest.EventConfigs/issues/1).

Comment on the issue to let people know that you will be working on it.

#### 2. Create your own fork of this repository

Click the "Fork" button in the top-right of this repository.

![](https://i.imgur.com/1dodbEh.png)

You'll now have your own copy of this repository that you can edit.

#### 3. Create a branch to do your work on

Click on "Branch", and type in the name of your new branch.
Choose something descriptive and relevant for the issue you are solving.

A suggested format is `boss-name/event-name`.

![](https://i.imgur.com/nfvPu3I.png)

#### 4. Make the necessary changes

You can either clone your repository to your machine and edit it using your favourite text editor / IDE,
or you can navigate to the file on GitHub and click the "Pencil" icon in the top-right to edit it in the browser.

Once you've previewed your changes, add a commit message and click "Commit Changes".

![](https://i.imgur.com/g7akYOK.png)

#### 5. Test your changes

You can test your changes on the [development version of Wipefest](https://wipefest-dev.herokuapp.com).

Find a fight to test your change on.
At the top of the page,
fill in the "Account" and "Branch" fields with the details of your GitHub account and branch,
and click "Set".

![](https://i.imgur.com/KYlITKd.png)

*For convenience, these values will be saved to your machine.
If you want to revert back to the live event configurations,
set "Account" to "JoshYaxley" and "Branch" to "master".*

The events view will reload, this time pulling data from your branch.

![](https://i.imgur.com/XZTJBAF.png)

Test your change on as many fights as appropriate,
to be sure that it is working.

#### 6. Create a pull request

On the home page of your repository,
click the "Compare & pull request" button.

![](https://i.imgur.com/hh4w4qA.png)

If there's anything I need to know to test the change,
be sure to note it here.
When you're ready, click "Create pull request".

![](https://i.imgur.com/nQbwHa5.png)

Go back to the original issue, and add another comment to let people know that you've solved it
(reference your pull request with a "#" and the number your pull request was given when you created it).

I'll test your change and merge it into the "master" branch, will will put it live.
You'll get a notification/email when your pull request has been merged!

Thanks for contributing :)
