## Day 13

# Commands Used and Screenshots of output

lsblk

<img width="482" height="200" alt="image" src="https://github.com/user-attachments/assets/575f11d9-4af1-477e-9599-82ed5c637d7c" />


df -h

<img width="467" height="145" alt="image" src="https://github.com/user-attachments/assets/9459a210-c8df-4fe3-8d59-f96436fb1617" />


pvs,vgs,lvs

<img width="235" height="63" alt="image" src="https://github.com/user-attachments/assets/bb211ed5-54dd-44d3-92aa-1f42363d3f50" />


pvcreate /dev/nvme1n1

<img width="388" height="62" alt="image" src="https://github.com/user-attachments/assets/440e7747-bd60-4470-88f2-262bfa0c5f8d" />


pvs

<img width="306" height="47" alt="image" src="https://github.com/user-attachments/assets/dfb6e569-e88d-44b2-b250-5d8de4f1580b" />


vgcreate devops-vg /dev/nvme1n1

vgs

<img width="355" height="73" alt="image" src="https://github.com/user-attachments/assets/ec46a939-2cc9-4036-ab2e-539f4e7f26d3" />


lvm> lvcreate -L 500M -n app-data devops-vg

<img width="329" height="35" alt="image" src="https://github.com/user-attachments/assets/3b38b2ef-6753-43ec-b8a5-93cda27d82bf" />


lvs

<img width="669" height="50" alt="image" src="https://github.com/user-attachments/assets/caa23453-22c3-4b06-8093-fcdf539f468d" />


mkfs.ext4 /dev/devops-vg/app-data

<img width="484" height="161" alt="image" src="https://github.com/user-attachments/assets/272fde20-59ce-4c9a-b475-4e5d59e4ea29" />


mkdir -p /mnt/app-data

mount /dev/devops-vg/app-data /mnt/app-data

df -h /mnt/app-data

<img width="515" height="79" alt="image" src="https://github.com/user-attachments/assets/44102f87-c4e4-445d-9b94-a1f80c6deaab" />


lvm> lvextend -L +200M /dev/devops-vg/app-data

<img width="797" height="65" alt="image" src="https://github.com/user-attachments/assets/18d5532d-d909-446a-9fa6-5533a9b97a83" />


resize2fs /dev/devops-vg/app-data

<img width="674" height="82" alt="image" src="https://github.com/user-attachments/assets/feafb2f5-8b11-4ded-808f-99be62215243" />


df -h /mnt/app-data

<img width="500" height="47" alt="image" src="https://github.com/user-attachments/assets/b8ef69aa-d804-43ee-92ae-8e7dca8364d7" />



# What I learned
Today I learned:

1> how to create Physincal Volume, Volume Group and Logical Volume.

2> how to format and mount disk

3> how to extend disk space






