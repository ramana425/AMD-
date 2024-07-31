# AMD-

Algorithm: Dynamic GPU Switching Based on Workload

1. Initialization:
   - Set a threshold FPS (T_FPS) below which the switch to external GPU (eGPU) should occur.
   - Monitor the current FPS (C_FPS).
   - Define a buffer period (B) to avoid frequent switching.
   - Initialize a timer (T).

2. Monitoring FPS:
   - Continuously monitor the C_FPS using the game/application's API or performance monitoring tool.

3. Decision Logic:
   - If C_FPS < T_FPS and eGPU is not active:
     - If T >= B:
       - Switch to eGPU.
       - Reset T.
     - Else:
       - Increment T by the elapsed time since last check.
   - If C_FPS >= T_FPS and eGPU is active:
     - If T >= B:
       - Switch to internal GPU (iGPU).
       - Reset T.
     - Else:
       - Increment T by the elapsed time since last check.
   - Else:
     - Reset T.

4. Switching Mechanism:
   - Implement system-specific commands/APIs to switch between iGPU and eGPU.
   - Ensure the current tasks and data are properly handled to avoid data loss during the switch.

5. Handling Edge Cases:
   - Include logic to handle scenarios where switching is not possible due to system constraints.
   - Provide user notifications during the switch for transparency.
