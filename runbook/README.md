# Guidance


## SequencedStartStopByTag_Parent.ps1

1. In portal, search Start/Stop VMs during off-hours, create a new solution. A pure new resource group is prefered
   see guidance at https://docs.microsoft.com/en-us/azure/automation/automation-solution-vm-management
   Note: Select a Pricing tier. Choose the Per GB (Standalone) option. Log Analytics has updated pricing and the Per GB tier is the only option.
   
2. slightly change SequencedStartStop_Parent to accept VMTtags, or create a new runbook.
   code at SequencedStartStopByTag_Parent.ps1
   
3. create new schedule for SequencedStartStop_Parent
	- Action: stop, VMTags: stopat10am    	(10 AM china time) 
	- Action: stop, VMTags: stopat10pm		(10 PM china time)
	
4. delete exist schedule task
   
   
## ScheduledStartStop_Parent.ps1

1.	All VMs will be stopped 

2. Add tag `autostop: no` to your VM or resource group if you don’t want runbook to stop your VM at night. If a resource group (RG) has this tag, all VM in that RG won’t be stopped.

## Mix

VMs with tags stopat10pm/stopat10am will be stopped at a specific time even though its RG has tag autostop:no