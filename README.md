Step A & B: Existing and Embedded Base
1. From the user uploaded list of locations falling within the analysis area, identify all existing transmitters and embedded base transmitters with an active project that cover at least one location.
2. Identify any embedded base sites without a carrier add project that are within the analysis area. Also include all embedded base sites within 10km of the analysis area.
3. Generate coverage for all transmitters in Step 2 using NPP PoD, if current coverage is not available.

Step C: SMDB Sites
1. Identify SMDB sites falling within the analysis area, including within a 10km buffer.
2. Eliminate SMDB sites which violate ISD (Intersite Distance) criteria with Step A+B+C sites
3. Generate coverage for each Step 2 transmitter using NPP POD.

Step D: New sites
1. Identify locations not covered by sites in Steps A, B, and C.
2. Using user defined ISD and min/max location counts (as specified as part of project creation), run DB scan clustering on the uncovered locations.
3. Ignore clusters where the centroid of the cluster violates the ISD constraint with sites from Steps A, B, and C.

