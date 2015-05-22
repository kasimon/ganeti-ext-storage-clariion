Clariion/VNX external storage module for ganeti

# Purpose

 This modules makes ganeti external storage module to work with HP EVAs Systems

# Prerequisites

 * naviseccli (download from EMC website)
 
# Installation

 * Copy this directory info a directory in the ExtStorage Providers search path
  (/srv/ganeti/extstorage, /usr/local/lib/ganeti/extstorage, /usr/lib/ganeti/extstorage,
   /usr/share/ganeti/extstorage)

 * Copy and complete clariion.conf in /etc/ganeti/extstorage/

 * Make sure the naviseccli is correctly set in the clariion.conf

 * Patch function NewUUID() in  /usr/share/ganeti/ganeti/utils/io.py to match this one :

        def NewUUID():
          """Returns a random UUID.
       
          @note: This is a Linux-specific method as it uses the /proc filesystem.
          @rtype: str
       
          """
          return ReadFile(constants.RANDOM_UUID_FILE, size=18).rstrip("\n")


 
 * (ganeti < 2.12) Patch function GenerateDiskTemplate() in lib/cmdlib/instance_storage.py :

          # Only for the Ext template add disk_info to params
          if template_name == constants.DT_EXT:
            params[constants.IDISK_PROVIDER] = disk[constants.IDISK_PROVIDER]
        +   params[constants.IDISK_NAME] = disk[constants.IDISK_NAME]

 * restart ganeti


# TODO

* VNX support - currently only Clariion devices are supported

