# Experiments and scenarios

This directory contains simulation launchers, configurations, scenes, and experiment-specific tools. For the retained manuscript analysis, start with the independent [reproducibility package](../reproducibility_package/README.md).

| Directory | Scope | Entry point |
|---|---|---|
| [`future_transport_2026/`](future_transport_2026/) | Separate prospective research campaigns, with recorded design and analysis decisions | [`PROTOCOL.md`](future_transport_2026/PROTOCOL.md) |
| [`intersection_radar_comm/`](intersection_radar_comm/) | Intersection scenarios with local sensing and V2X reception treatments | `scripts/run.sh` |
| [`truck_lane_change/`](truck_lane_change/) | Lane-changing and warning-response scenarios | `scripts/run.sh` |
| [`intersection_crash/`](intersection_crash/) | Junction priority-conflict scenarios | `scripts/run.sh` |
| [`intersection_v2x_awareness/`](intersection_v2x_awareness/) | Alternative intersection-awareness implementation | `scripts/run.sh` |
| [`cpm_perception/`](cpm_perception/) | Collective perception and sensor/communication treatments | `scripts/run.sh` |
| [`compare_tech/`](compare_tech/) | Communication-stack comparisons | `scripts/run.sh` |
| [`operational/`](operational/) | Launchers for inherited ms-van3t examples | `<scenario>/run.sh` |
| [`strict_sionna_vkr/`](strict_sionna_vkr/) | Historical Sionna scenarios, manifests, and batch utilities | `scripts/` |
| [`raw/`](raw/) | Additional raw-output scenario launchers | Scenario-specific scripts |

Launchers have scenario-specific environment and directory assumptions. Consult their local instructions and [DEVELOPMENT.md](../DEVELOPMENT.md) before execution. Existing path contracts are retained for compatibility.

The prospective protocols and older demonstrations are not interchangeable with the 140 EVA and 27 intersection records in the manuscript package. Preserve cohort identifiers, configuration, source revisions, and inclusion rules when running new experiments.

Additional retained records are under [`runs/`](../runs/README.md). General analysis and plotting utilities are under [`tools/`](../tools/README.md).
