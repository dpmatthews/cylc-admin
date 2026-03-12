# Project Planning: 2026/27

This document attempts to list the main work planned for the next year and to
explore priority topics under consideration beyond that.

## Priorities for the next year

1. Isolated start-up and shut-down graphs (priority for ESNZ operations). See
   [cylc-flow#7020](https://github.com/cylc/cylc-flow/issues/7020).

1. Replace suicide triggers with expire triggers. This is already available as
   an experimental feature but needs a little work before it becomes the default.
   See [cylc-flow#7175](https://github.com/cylc/cylc-flow/issues/7175).

1. Address oustanding issues identified during Met Office operational
   implementation (see
   [MO Operator Priorities project](https://github.com/orgs/cylc/projects/6/views/1)).
   In particular:

   * Performance issues with large `cylc set` operations. See
     [cylc-flow#7183](https://github.com/cylc/cylc-flow/issues/7183).
   * Viewing large log files. See
     [cylc-uiserver#421](https://github.com/cylc/cylc-uiserver/issues/421).
   * Task multiple selection (e.g. for group triggering). See
     [cylc-ui#434](https://github.com/cylc/cylc-ui/issues/434).

1. Support CPU and memory profiling (finishing off work started in 2025). See
   [cylc-flow#6663](https://github.com/cylc/cylc-flow/pull/6663).

1. Graph view family collapsing - make the graph view usable for large, complex
   workflows (finishing off work started in 2024). See
   [cylc-ui#1130](https://github.com/cylc/cylc-ui/issues/1130).

1. Port cylc review to Python 3. This is a short term fix to remove our
   dependency on Cylc 7 / Python 2 whilst we decide what should replace cylc
   review longer term. See
   [cylc-uiserver#755](https://github.com/cylc/cylc-uiserver/pull/755).

1. Complete the port of rose edit to Python 3. An initial release is available
   but further work is require to reach the point where we can fully retire the
   Python 2 version.

## Potential future priorities

This section lists the main development areas currently under consideration as
future priorities (without attempting to say what order they should be tackled
or when since this will depend on future resourcing and user feedback).

### Data driven workflows

Topics pertaining to how inputs/outputs are defined and exchanged between tasks/workflows.

* __Context__: As workflow and suite (i.e, "suite" a collection of inter-dependent workflows) complexity increases, the matter of interfaces increases in priority. There is a growing emphasis on data provenance, traceability and observability, all problems which are hard to resolve at present due to poor visibility of data flow within and between Cylc workflows. Data driven paradigms also have benefit to workflow developers and allow for more decoupled workflows.

* __Action__: There are several things we can do to formalise inputs/outputs in Cylc and facilitate the exchange of metadata (whilst continuing to offer existing paradigms of course).

### Cloud deployment patterns

Topics pertaining to reducing the barriers to the deployment of Cylc into cloud environments.

* __Context__: The cloud has subtly re-defined many aspects of deployment. Cylc doesn't always naturally fit the patterns that cloud engineers are used to which can cause friction (round pegs and square holes).

* __Action__: There are several ways (both big and small) in which we can reduce this friction. There may also be ways in which we can reduce the cost of Cylc deployments. Ultimately, it would be brilliant if we could get to the point where we are able to offer a Cylc cloud platform as a configuration (e.g, Helm chart of whatnot) that others could easily modify and deploy.

### CD for Cylc workflows

Providing tooling for the continuous deployment of Cylc workflows and reducing barriers to the automation of workflow lifecycle events.

* __Context__: There has been a long-term trend away from operator-lead deployment, towards continually deployed systems with dev-opps overseers. This is the paradigm that many teams approaching Cylc will be expecting, however, Cylc is reliant on manual interventions and does not provide the right guarantees for these purposes. This generates friction and forces teams to develop extensive pipelines to "puppet" Cylc (i.e, orchestrating the orchestrator).

* __Action__: Provide tooling within Cylc to manage workflow lifecycle and ensure important operations (namely graph changes) can be actioned in an automated manner.

### Observability

Topics pertaining to improving the observability of Cylc tasks/workflows/suites/deployments.

* __Context__: Similar to (1), complexity is going up which means observability is going up, both in importance and also abstraction (e.g, observability within one workflow vs observability within one "suite" of workflows, vs observability within one site). There is a great wealth of mature tooling for observability and telemetry. The "Analysis View" and "Cylc Profiler" also fit this topic which may extend to things like workflow optimisation and cost analysis.

* __Action__: Consider how Cylc should integrate with observability tooling (e.g, consider offering Prometheus / Open Telemetry / whatever endpoints?) and how telemetry could be exposed within Cylc tooling (e.g, Grafana on the GUI dashboard?).

### Jupyter integration

Topics pertaining to the integration of Cylc with the Jupyter ecosystem.

* __Context__: Jupyter is rapidly evolving, in a couple of cases, we have fallen a step behind them. The question of how to integrate Jupyter Lab / Cylc GUI has yet to be solved. Jupyter provides a lot of power and some very attractive possibilities which we are yet to truly exploit.

* __Action__: Play catch-up as needed and improve the inter-operability of Cylc / Jupyter Lab.

### Multi-user access

Topics around how groups of users interact with Cylc workflows.

* __Context__: A long running matter, much of the fundamentals are in place now, but there are still some things outstanding.

* __Action__: Continuing effort in this area.

### Workflow documentation

Topics pertaining to how we document tasks, families and workflows and how we provide access to this documentation.

* __Context__: Workflow documentation has historically been a weakness of Cylc forcing sites to develop external solutions or just live-without, however, we are now in a good position to push this forward with a native Cylc solution.

* __Action__: Develop in-GUI and Spinx documentation functionalities for Cylc workflows.

### Offline data

Expanding the GUI view beyond the n-window and extracting data from stopped workflows.

* __Context__: The n-window is restrictive and not the best solution for many use cases. Cylc Review is there to mop up the things the GUI can't do, but this isn't the situation we want long-term.

* __Action__: Develop an alternative windowing system, generate an SQL backend allowing the UIS to front "offline" data and develop any required robustness / performance enhancements required for the GUI to handle this influx of data.

### Plugin infrastructure

Topics pertaining to Cylc plugins (including main-loop, xtriggers, workflow configuration tools, etc).

* __Context__: Plugins are a key tool to boosting the functionality and integration of Cylc without necessarily having to provide all of the development effort ourselves. We have a small set of plugin hard-points, many use cases require the development (and documentation!) of further interfaces. We could also do with some standardisation as some plugins are loaded via entry-points, others are loaded via FS locations, some via either/both. Questions to be answered such as how do we bundle plugins with workflows, and how do we define plugin inter-dependence (required initially for workflow configuration plugins).

* __Action__: Develop new plugin interfaces, standardise plugins better and provide more comprehensive documentation to plugin developers.

### UX

Topics pertaining to GUI / Tui.

* __Context__: Obvious.

* __Actions__: Continued development, dur!

### Stability, performance and caveats

Topics pertaining to ongoing maintenance and robustness improvements.

* __Context (performance)__: Cylc has certain scaling limits, on the scheduler, UIS and GUI respectively. Some of these limits are pain points already, others will become pain points as we start to receive offline data in the GUI and as workflow complexity continue to increase.

* __Context (caveats)__: Many Cylc interventions come with caveats making it hard to provide generic instructions. Some of these are things we can iron out. Previous work such as group-trigger has gone a long way in this regard, but there are matters remaining.

* __Context (robustness)__: Improving the robustness of Cylc from the perspective of workflows (crash tolerance, etc), and workflow deployments (Cylc server management, FS stability, DB issues, etc).

* __Context (SoD)__: SoD migration has involved a lot of re-jigging, especially in the interventions which had to change drastically to continue to support Cylc 7 use cases. We are mostly there now, but there are some lingering matters left in the woodwork.

* __Action__: A few issues already in the pipelines, some interventions may need discussion, ongoing profiling and optimisation, etc.

### Housekeeping

Built-in file housekeeping – to deprecate rose prune. This is essential for any
long-running cycling workflows so really ought to be a core feature. Also, rose
prune doesn't work well with some Cylc features (e.g. `job/log` directory
symlinking). See [cylc-flow#1159](https://github.com/cylc/cylc-flow/issues/1159).

### Polling re-design

Re-engineer task polling – this has evolved over time to be difficult to
understand and maintain, and has several nasty issues (e.g.
[cylc-flow#3436](https://github.com/cylc/cylc-flow/issues/3436) and
[cylc-flow#4513](https://github.com/cylc/cylc-flow/issues/4513)).

### Single job for multiple tasks

Many workflows contain lots of small tasks which could be run much more
effeciently if combined into a single job. We currently use rose bunch to
partially achieve this in some cases but there is potential for a much more
powerful and flexible solution built into Cylc. See
[cylc-flow#2754](https://github.com/cylc/cylc-flow/issues/2754).

### Miscellaneous

Priority developments which needs need to be covered somewhere (not sure where to put them yet):

* Offline data: [cylc-uiserver#378](https://github.com/cylc/cylc-uiserver/issues/378)
* Static graphs: [cylc-ui#82](https://github.com/cylc/cylc-ui/issues/82)
* Source workflows: [cylc-ui#548](https://github.com/cylc/cylc-ui/issues/548)

Topics we have listed previously (do we still want these listed on the priority list and, if so, are they part of wider topics?):

* Advanced Cycling with RRULE – some cycling use cases are difficult or impossible with ISO8601 recurrence expressions. See [cylc-flow#2398](https://github.com/cylc/cylc-flow/issues/2398)
* Built-in support for sub-workflows – some use cases demand this; currently difficult to design, implement, and manage. See [cylc-flow#6584](https://github.com/cylc/cylc-flow/issues/6584)
* Adapt Cylc to cloud architectures – we don’t yet know Partner requirements or timelines in this regard.
* More flexible, modular workflow design (e.g. via a Python API as an alternative to config file with Jinja2 templating). See [cylc-flow#1962](https://github.com/cylc/cylc-flow/issues/1962).
