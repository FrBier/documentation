Programmer Interface: Control Registers
---------------------------------------

The System Control Module implements the :ref:`sec:spec:api:base_register_map`.
Additionally, it implements the following control registers for module-specific functionality.


.. tabularcolumns:: |p{\dimexpr 0.20\linewidth-2\tabcolsep}|p{\dimexpr 0.30\linewidth-2\tabcolsep}|p{\dimexpr 0.50\linewidth-2\tabcolsep}|
.. flat-table:: SCM Register Map
  :widths: 2 3 5
  :header-rows: 1

  * - address
    - name
    - description

  * - ``0x0200``
    - ``SYSTEM_VENDOR_ID``
    - Vendor ID

  * - ``0x0201``
    - ``SYSTEM_DEVICE_ID``
    - Device ID

  * - ``0x0202``
    - ``NUM_MOD``
    - Debug module count

  * - ``0x0203``
    - ``MAX_PKT_LEN``
    - Maximum packet length

  * - ``0x0204``
    - ``SYSRST``
    - System Reset


System ID (``SYSTEM_VENDOR_ID``)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Address: 0x0200
- Reset Value: *implementation specific*
- Access: read-only

The vendor ID identifies the entity creating/producing the device (e.g. the chip) that contains the OSD implementation.
Vendor IDs are assigned by the Open SoC Debug Project.
Unassigned vendor IDs may not be used.

.. note::
  A list of assigned vendor IDs is available online at :ref:`sec:idregistry:vendorids`.


Device ID (``SYSTEM_DEVICE_ID``)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Address: 0x0201
- Reset Value: *implementation specific*
- Access: read-only

Number identifying the device (e.g. the chip) that contains the OSD implementation.
The device ID must be uniquely describe the device design as it is visible through the debug system.

Device IDs are assigned by the device vendor, identified by ``SYSTEM_VENDOR_ID``.


Debug module count (``NUM_MOD``)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Address: 0x0202
- Reset Value: *implementation specific*
- Access: read-only

The number of debug modules in addition to the HIM and SCM modules.
Since all module addresses must be continguous, this value also describes the highest module address available in the debug system as ``NUM_MOD`` + 1.


Maximum packet length (``MAX_PKT_LEN``)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Address: 0x0203
- Reset Value: *implementation specific*
- Access: read-only

Maximum length of debug packets in 16 bit words, including all headers.

.. todo::
  Specify minimum required value.


System reset (``SYSRST``)
^^^^^^^^^^^^^^^^^^^^^^^^^

- Address: 0x0204
- Reset Value: *implementation specific*
- Access: read-only

Reset the (parts) of the system.

.. tabularcolumns:: |p{\dimexpr 0.10\linewidth-2\tabcolsep}|p{\dimexpr 0.30\linewidth-2\tabcolsep}|p{\dimexpr 0.10\linewidth-2\tabcolsep}|p{\dimexpr 0.10\linewidth-2\tabcolsep}|p{\dimexpr 0.40\linewidth-2\tabcolsep}|
.. flat-table:: Field Reference: ``CONF``
  :widths: 1 3 1 1 4
  :header-rows: 1

  * - Bit(s)
    - Field
    - Access
    - Reset Value
    - Description

  * - 15:2
    - ``RES``
    - r/w
    - 0x0
    - **Reserved**

  * - 1
    - ``CPU_RST``
    - *impl.-spec.*
    - w
    - **CPU Reset**

      Reset all units executing code (e.g. CPUs) in the system.

      **0b0: Deactivate the CPU reset**
        The CPU reset signal is set to the deactivated state.

      **0b1: Activate the CPU reset**
        The CPU reset signal is set to the activated state, resetting all CPUs.
        The reset signal must be explicitly deactivated again with another register write.

  * - 0
    - ``SYS_RST``
    - *impl.-spec.*
    - w
    - **System Reset**

      Put the device, excluding the debug system.

      **0b0: Deactivate the system reset**
        The system reset signal is set to the deactivated state.

      **0b1: Activate the system reset**
        The system reset signal is set to the activated state, resetting the device.
        The reset signal must be explicitly deactivated again with another register write.
