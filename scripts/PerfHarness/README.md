# CoreFxLab Perf Test Harness

This project contains a simple harness to run performance tests and measure the
results.

## Run the Performance Tests

1. Make sure all of the tests have been restored
   (`dotnet restore <path-to-tests-dir>`)

2. Restore this project
   (`dotnet restore`)

3a. Run the harness--make sure to use the release configuration
   (`dotnet run -c Release`)
   
3b. To run specific tests only, pass in the type names to the harness (this run types found in any of the assemblies):
   (`dotnet run -c Release -- --perf:typenames name1 [name2] [...]`)
   
3c. To run specific tests found in a specific assembly only, pass in the assembly name and type names to the harness:
   (`dotnet run -c Release -- --assembly Benchmarks --perf:typenames name1 [name2] [...]`)

## Add a New Performance Test

When adding a new xunit-performance compatible test project, simply make the
following changes to enable it to run using this harness:

* Add a project dependency in this project's `project.json` referencing the new
  test project.

* Add the new element to the array returned by `GetTestAssemblies()` inside
  `PerfHarness.cs`. The element should be the name of the perf test project
  assembly, excluding the file extension.
