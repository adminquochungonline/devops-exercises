# AWX Project - Scenario 1 (cai dat package)

Thu muc nay chua playbook + inventory de AWX keo ve tu Git va chay.
**Khong** chua secret; thong tin SSH khai bao trong AWX Credential.

## File
- `scenario1_packages.yml` - playbook cai nginx, git, curl (Scenario 1).
- `inventory.ini` - inventory tro toi `target-node` (khong co user/password).

## Cach cau hinh tren AWX

1. **Project**
   - Source Control Type: `Git`
   - Source Control URL: URL cua repo nay
   - Source Control Branch: branch chua thu muc nay
   - Sau khi luu, AWX se `sync` (keo code ve).

2. **Credential** (loai *Machine*)
   - Username: `ansible`
   - Password: *(mat khau SSH cua user ansible tren target-node - nhap truc tiep trong AWX)*
   - Privilege Escalation: `sudo` (de `become` hoat dong)

3. **Inventory**
   - Tao Inventory moi, them Source loai *Sourced from a Project*,
     tro toi Project o buoc 1 va file `ansible-k3s/awx-project/inventory.ini`.
   - Hoac tao host thu cong: `target-node` voi variable
     `ansible_host=target-node.ansible.svc.cluster.local`.

4. **Job Template**
   - Inventory: chon inventory o buoc 3
   - Project: chon project o buoc 1
   - Playbook: `ansible-k3s/awx-project/scenario1_packages.yml`
   - Credential: chon credential o buoc 2
   - Luu va bam **Launch**.

> Luu y: pod AWX (namespace `awx`) va target-node (namespace `ansible`) nam trong cung cluster k3s,
> nen AWX goi toi `target-node.ansible.svc.cluster.local` qua DNS noi bo duoc.
