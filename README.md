## About this fork

This project was forked to extend the OSRM service to support indoor routing.
Changes are primarily around repurposing metadata to communicate building and floor identifiers, adding parameterization of some constants, and preventing collapse of steps required for indoor navigation.

To build, run `build-local.bat`.  Note after the first build you can uncomment the `SET LOCAL_DEV=1` line to avoid re-downloading dependencies.  The results are written to `osrm_Release.zip`.

To run on windows, you will need to unzip the package and edit the `.stxxl.txt` file to something like `disk=D:\Temp\stxxl,100,memory`

To process a data file and run the server against it:
```
osrm-extract data.osm -p profile-name.lua
osrm-contract data.osrm
osrm-routed data.osrm --port port_no
```
The WRLD routing service defines a `profile-indoor.lua` and `profile-outdoor.lua` which configure input processing.

## About

The Open Source Routing Machine is a high performance routing engine written in C++11 designed to run on OpenStreetMap data.

## Current build status

| build config | status |
|:-------------|:-------|
| Linux        | [![Build Status](https://travis-ci.org/Project-OSRM/osrm-backend.png?branch=master)](https://travis-ci.org/Project-OSRM/osrm-backend) |
| Windows      | [![Build status](https://ci.appveyor.com/api/projects/status/4iuo3s9gxprmcjjh)](https://ci.appveyor.com/project/DennisOSRM/osrm-backend) |
| Coverage     | [![codecov](https://codecov.io/gh/Project-OSRM/osrm-backend/branch/master/graph/badge.svg)](https://codecov.io/gh/Project-OSRM/osrm-backend) |

## Contact

- IRC: server `irc.oftc.net`, channel: `#osrm` (see: `https://www.oftc.net`, and for a webchat: `https://webchat.oftc.net`)
- Mailinglist: `https://lists.openstreetmap.org/listinfo/osrm-talk`

## Building

For instructions on how to [build](https://github.com/Project-OSRM/osrm-backend/wiki/Building-OSRM) and [run OSRM](https://github.com/Project-OSRM/osrm-backend/wiki/Running-OSRM), please consult [the Wiki](https://github.com/Project-OSRM/osrm-backend/wiki).

To quickly try OSRM use our [free and daily updated online service](http://map.project-osrm.org)

## Documentation

### Full documentation

- [osrm-routed HTTP API documentation](docs/http.md)
- [libosrm API documentation](docs/libosrm.md)

### Quick start

Building OSRM assuming all dependencies are installed:

```
mkdir -p build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
cmake --build .
sudo cmake --build . --target install
```

Loading preparing a dataset and starting the server:

```
osrm-extract data.osm.pbf -p profiles/car.lua
osrm-contract data.osrm
osrm-routed data.osrm
```

Running a query on your local server:

```
curl http://127.0.0.1:5000/route/v1/driving/13.388860,52.517037;13.385983,52.496891?steps=true&alternatives=true
```

### Running a request against the Demo Server

First read the [API usage policy](https://github.com/Project-OSRM/osrm-backend/wiki/Api-usage-policy).

Then run simple query with instructions and alternatives on Berlin:

```
curl https://router.project-osrm.org/route/v1/driving/13.388860,52.517037;13.385983,52.496891?steps=true&alternatives=true
```

## References in publications

When using the code in a (scientific) publication, please cite

```
@inproceedings{luxen-vetter-2011,
 author = {Luxen, Dennis and Vetter, Christian},
 title = {Real-time routing with OpenStreetMap data},
 booktitle = {Proceedings of the 19th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems},
 series = {GIS '11},
 year = {2011},
 isbn = {978-1-4503-1031-4},
 location = {Chicago, Illinois},
 pages = {513--516},
 numpages = {4},
 url = {http://doi.acm.org/10.1145/2093973.2094062},
 doi = {10.1145/2093973.2094062},
 acmid = {2094062},
 publisher = {ACM},
 address = {New York, NY, USA},
}
```

