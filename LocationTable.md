# Introduction #
The LocationTable (aorglu\_loctable class) stores location information for nodes. It will need to be updated with:
  1. The location information for nodes form which it received a RREP or RREQ.
  1. The location information of one-hop neighbours (via HELLO messages).

The LocationTable will include an expiration timer that is controlled by the constant LOC\_CACHE\_EXP (see aorglu/aorglu.h for definition.) If this is defined as -1, the cache entries will never expire.

This cache should not be confused with the ChatterCache. The ChatterCache is used for keeping track of nodes with which it has been recently communicating data with. This Cache is used to keep track of which nodes LUDP packets should be sent to to update the LocationTable.

# Details #

The LocationTable has been implemented in the files: _aorglu`_`loctable.h_ and _aorglu`_`loctable.cc_.

The LocationTable is a member function called "loctable" in the AORGLU Agent. This class variable holds the location table entries for the current AORGLU node.

## Available Methods ##
  * **aorglu`_`loc\_entry`*` head()** - Return the pointer to the head of the list.

  * **void print()** - Print out the current loctable to stderr.

  * **aorglu`_`loc\_entry`*` loc\_add(nsaddr`_`t id, double X, double Y, double Z)** - If no entry for the given ID exists, it will create a new entry in the loctable with the given parameters. Otherwise, the location the specified node is updated and the expiration timer renewed.

  * **void loc\_delete(nsaddr`_`t id)** - Deletes the given node location entry.

  * **aorglu`_`loc\_entry`*` loc\_lookup(nsaddr`_`t id)** - Looks-up and returns the pointer to the entry in the list with the given id. If no entry exits, NULL is returned.