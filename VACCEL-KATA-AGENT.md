### Add Guest vAccel device to Kata Container

The Guest VM loads the vAccel virtio module and exposes a character device to userspace under /dev/accel.
The kata-agent needs to expose this device to the container. To do so, kata-agent needs to:

- Be aware of the device's major/minor numbers and path
- Add this information in the OCI spec from which the container is created.

We implement addAccelDevice() function which call the syscall stat in order to find the major/minor
number of guest's /dev/accel device. We append the OCI spec with these information before starting
the container. 

We plan to:

- create a vAccel driver type and a handler and append the OCI request sent from the host (kata-runtime).
- implement it for the new kata (rust) agent (Kata Containers 2.x)
