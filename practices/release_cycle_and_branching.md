Odyn Release Cycle
------------------
Period: Monthly

The goal is to keep up a steady cadence and publish a release of Odyn every
month.  Releases will be published on our website here:

    http://odyn.io/devzone/release_notes.html

Releases only include features that have been code reviewed and tested.

Releases are made by "tagging" the master branch of every repo that is
participating in the release.

    git tag -a v15.04.03 -m "Release Apr 03 2015"

    git push origin v15.04.03

There will also be some work to package the release and post it on the website.
I'm still figuring out the details, but I'd like it to be easy (i.e., just run
a release script).


Release Versioning Across Repos
-------------------------------
Odyn is made up of several repositories.

On the one hand, each repository is a separate project that could follow its
own release schedule and versioning scheme.

On the other hand, Odyn can be viewed holistically as a complete system whose
components work together seamlessly.  Taking this view, it would be good to be
able to tell, at a glance, if all the components you are using will play nicely
together.

The solution is to use the date as the version number.  For example, a release
made on Apr 3, 2015 will be called "v15.04.03".

If you are using v15.04.03 of the C client, and v15.04.03 of the Server, you
can be confident that they work together.

If the C client does not change for a month then there is no need to release
it.  So in May, we might have v15.04.03 is the latest C client, whereas
v15.05.01 is the latest version of the Server.    These will be compatible, but
we will have to communicate this some other way (i.e. in the release notes).

Then in June, if we release both components again, the release numbers will
once again be in sync: v15.06.14 for both client and server (for example).

I do not anticipate ever having two releases on the same day.  If we need to,
for example, hotfix a release that was just published, we can add a letter
"v15.06.14b" or nanoversion "v15.06.14.01".


Development Cycle
-----------------
Development will be decoupled from the release cycle.

Some features might take 1 day to implement, whereas others might take 6 months.

Development will take place in feature branches, for example
"feature-device-filtering".  When a feature is completed, reviewed, and
demonstrably working, it can merged into a release integration branch, for
example "r15.04.03-dev".  When we are ready to make a release, all changes in
"r15.04.03-dev" will be reviewed (holistically) and then merged into "master".


Hot Fixes
---------
Critical hot fixes may be developed in a "hotfix-" branch and merged directly
into master after review.  Then a new release can be created by tagging
"master".

Merge Diagram
-------------

    Arrows ( <--- ) represent permitted "git merge" directions.
    Double arrows ( <=== ) mean code review should happen before the merge.

         === hotfix-BARBAZ
       //
      v
    master <=== rXX.YY.ZZ-dev <=== feature-FOOBAR
                     |                   ^
                     |                   |
                      -------------------
