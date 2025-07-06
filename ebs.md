### 📄 **EBS Setup Guide – Bash Commands**

---

#### ✅ **Part 1: Launch EC2 and Attach EBS Volume**

1. **Create EC2 instance** (via AWS Console) — Use Amazon Linux 2 or Ubuntu.
2. **Create EBS Volume** from AWS Console:

   * Go to **Elastic Block Store → Volumes → Create Volume**.
   * Choose same **Availability Zone** as the EC2 instance.
   * Size: e.g., 15 GiB.
3. **Attach Volume to EC2**:

   * Go to **Volumes → Select Volume → Actions → Attach Volume**.
   * Choose your instance, device name like `/dev/xvdb`.

---

#### ✅ **Part 2: On EC2 Terminal – Bash Commands**

```bash
# Step 1: Check available disks
lsblk

# Step 2: Check if volume is formatted
sudo file -s /dev/xvdb
# If output is like "/dev/xvdb: data", it means it's unformatted

# Step 3: Format the volume with XFS
sudo mkfs -t xfs /dev/xvdb

# Step 4: Create a mount point directory
sudo mkdir -p /mnt/cc

# Step 5: Mount the volume
sudo mount /dev/xvdb /mnt/cc

# Step 6: Verify that the mount was successful
df -h

# Step 7: Get UUID of the volume
sudo blkid /dev/xvdb
# Output will contain something like:
# UUID="your-uuid-here"

# Step 8: Make mount persistent across reboots
sudo nano /etc/fstab
# Add this line at the bottom (replace UUID):
# UUID=your-uuid-here /mnt/cc xfs defaults,nofail 0 2

# Step 9: Test fstab entry for errors
sudo mount -a
# No output means it's correct

# Step 10: Reboot and verify
sudo reboot
# After reconnecting:
df -h
```

---

#### ❌ **Detach the Volume (When Done)**

```bash
# Step 1: Check mount status
df -h

# Step 2: Unmount the volume
sudo umount /mnt/cc

# Step 3: Go to AWS Console → Volumes → Select → Actions → Detach Volume
```

