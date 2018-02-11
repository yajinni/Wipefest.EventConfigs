# Wipefest Event Configurations

## Where are we?

When [Wipefest](https://www.wipefest.net/) constructs the events view, it:

* Loads the relevant configurations from this repository
* Builds a [Warcraft Logs](https://www.warcraftlogs.com/) filter based on these configurations
* Queries the [Warcraft Logs API](https://www.warcraftlogs.com/v1/docs) using this filter
* Using the same configurations, decides how to convert the returned Warcraft Logs events into Wipefest events
* Renders these events

#### [Examples](docs/examples.md)
#### [Specification](docs/specification.md)
#### [Contribute](docs/contribute.md)