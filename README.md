# AMD-

Algorithm: Dynamic GPU Switching with SMPS Control
Initialization:

Set a threshold FPS (T_FPS) below which the switch to external GPU (eGPU) should occur.
Monitor the current FPS (C_FPS).
Define a buffer period (B) to avoid frequent switching.
Initialize a timer (T).
Monitoring FPS:

Continuously monitor the C_FPS using the game/application's API or performance monitoring tool.
Decision Logic:

If C_FPS < T_FPS and eGPU is not active:
If T >= B:
Switch to eGPU.
Turn on the SMPS for the eGPU.
Reset T.
Else:
Increment T by the elapsed time since the last check.
If C_FPS >= T_FPS and eGPU is active:
If T >= B:
Switch to internal GPU (iGPU).
Turn off the SMPS for the eGPU.
Reset T.
Else:
Increment T by the elapsed time since the last check.
Else:
Reset T.
Switching Mechanism:

Implement system-specific commands/APIs to switch between iGPU and eGPU.
Ensure the current tasks and data are properly handled to avoid data loss during the switch.
SMPS Control:

Implement commands to control the SMPS for the eGPU.
Ensure the SMPS is safely turned on/off with proper delays to avoid damage.
Handling Edge Cases:

Include logic to handle scenarios where switching is not possible due to system constraints.
Provide user notifications during the switch for transparency.Implementation Notes:
Performance Monitoring: Use tools like NVIDIA's NVAPI, AMD's ADL, or DirectX Diagnostic Tool to monitor FPS.
System Commands: Use system-specific commands or APIs to handle GPU switching. For example, NVIDIA Optimus or AMD's equivalent can help in managing these switches.
SMPS Control: Use GPIO pins, relays, or specific power management APIs to control the SMPS. Ensure you account for any hardware-specific delays or requirements.
User Notifications: Implement a user-friendly way to notify the user about the GPU switch and SMPS status, such as desktop notifications.
This algorithm ensures efficient use of power by turning off the SMPS for the external GPU when it is not needed and dynamically switches based on the workload demands. Adapt the implementation details to suit your specific hardware and software environment.
