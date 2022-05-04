# CDS views for testing cyclic dependency

Inspired by: [ABAP CDS - Cyclical Dependencies](https://help.sap.com/doc/abapdocu_751_index_htm/7.51/en-us/abenddic_cds_cycle_problems.htm)

The example in the link above contains 3 CDS views which depend on each other by association. This is not a problem, because abapGit can pull and activate them. However one of the CDS view was altered so that there is a cyclic dependency which is not discovered by syntax checker. Everything is activated in the original system, but it cannot be pulled, nor activated in the target system using abapGit. 

This repo contains following CDS views:
 - **zja_test_view1**: has assocation which is dependent on zja_test_view2
 - **zja_test_view2**: has assocation which is dependent on zja_test_view3. It also has cyclic dependency created by union with zja_test_view1 (see note below)
 - **zja_test_view3**: has assocation which is dependent on zja_test_view1

Note: We use union, because when we directly use zja_test_view1 in the first select, then the cyclic dependency is discovered by syntax check: *"Recursive View Definitions are not supported"*.
