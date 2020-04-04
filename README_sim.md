One can simulate running of nvidia-dcgm-pbs connector on a node without GPUs.
It supports health-check and reporting of gpu stats. 
It does not currently support diagnostic check.
There are no changes to the python hook script.
This package contains a sample gpu telemetry data for a run using two gpus on single node and 4 gpu K800 nvidia gpu data to be used to simulate nvidia-smi command.
It does not support disabling of gpu telemetry like energyConsumed ie even if you disable collection of data for energyConsumed by setting report_usage to false it still shows data for energyConsumed. This is because sample gpu telemetry data contains dummy data for energyConsumed. You can simulate disabling it by removing the data from sample data by hand.

The package now consists of additional folder called PBS_scripts_sim containing wrappers and dummy data.
The folder should be kept in same location where the connector package is untarred.

-------------------
Installation Steps:
-------------------
- Follow instructions to install the connector as described in the readme. 
  Note that ngpus resource and gpu telemetry resources should be defined by now as well as the hook is setup. Also resources line in sched_config must have ngpus and scheduler restarted.
- Export the following from the terminal being used to install the package.

    export GPU_GROUP_ID_START_VALUE=100

  Note that the value used here is totally random and has no bearing on results at all.
- Set ngpus value on the node to be equal to that of the nvidia gpu data.
- Set 'run_diagnostic_check' to false in json config file.
- Change 'path_to_pbs_scripts' to point to PBS_scripts_sim.
  Note that path to data files is relative to this path.
- Set 'using_cgroups' to false
- Check if 'exclude_hosts' and/or 'run_only_on_hosts' needs a look.
- Import the modified json config file.

-----------------
Data Setup Steps:
-----------------
- Perform these steps before Installation step #2.
- If /usr/bin/nvidia-smi is already installed then make a soft link as PBS_scripts_sim/nvidia-smi or copy nvidia-smi in /usr/bin directory with execute permission.
  Note that this script will simply output the sample gpu telemetry data.
- Check nvidia gpu data in PBS_scripts_sim/sim_data/nvidia-smi-data.
  Add more gpus or reduce gpus to suit your requirement.
  Remember to match number of gpus in <attached_gpus>. gpu_id or its order has no bearing on the results.
- Check sample gpu telemetry data in PBS_scripts_sim/sim_data/nvidia_get_resources_used_data.
  Change it to include more gpus.
  The sample data contains dummy telemetry collected for two gpus on a single node.
