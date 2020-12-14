# Orb Development

Orbs are shipped as individual `orb.yml` files, however, to make development easier, it is possible to author an orb in _unpacked_ form, which can be _packed_ with the CircleCI CLI and published.

The default `.circleci/config.yml` file contains the configuration code needed to automatically pack, test, and deploy and changes made to the contents of the orb source in this directory.

## @orb.yml

This is the entry point for our orb "tree", which becomes our `orb.yml` file later.

Within the `@orb.yml` we generally specify 4 configuration keys

**Keys**

1. **version**
    Specify version 2.1 for orb-compatible configuration `version: 2.1`
2. **description**
    Give your orb a description. Shown within the CLI and orb registry
3. **display**
    Specify the `home_url` referencing documentation or product URL, and `source_url` linking to the orb's source repository.
4. **orbs**
    (optional) Some orbs may depend on other orbs. Import them here.

## See:
 - [Orb Author Intro](https://circleci.com/docs/2.0/orb-author-intro/#section=configuration)
 - [Reusable Configuration](https://circleci.com/docs/2.0/reusing-config)

## Publishing process

Job approval requires a CircleCI  `Personal Access Token` to be set in the CIRCLE_TOKEN environment variable within the `orb-publishing` context.

The automated process is triggered by a commit message containing [semver:patch|minor|major|skip]

e.g. [semver:patch]

Manual process:

    circleci orb create avidaml/service
    circleci orb validate ./src/@orb.yml
    circleci orb publish ./src/@orb.yml avidaml/service@dev:alpha
    circleci orb publish promote avidaml/service@dev:alpha major