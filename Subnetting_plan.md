# Subnetting Plan for Growing Organization

## 1. Identify Subnet Requirements:

### Departments:
- Finance
- Human Resources
- Sales
- Marketing
- IT
- Operations

### Future Growth:
- Plan for at least 50% growth in each department over the next five years.

### Network Topology:
- Centralized data center for servers.
- Each department has its own floor in the office building.

---

## 2. Allocate IP Addresses:

### Subnets:
- Finance: 50 hosts
- Human Resources: 30 hosts
- Sales: 70 hosts
- Marketing: 40 hosts
- IT: 100 hosts
- Operations: 80 hosts

**Total Subnets Required**: 6

---

## 3. Subnet Masking:

### Subnet Masks:
- Finance: /26 (255.255.255.192)
- Human Resources: /27 (255.255.255.224)
- Sales: /25 (255.255.255.128)
- Marketing: /26 (255.255.255.192)
- IT: /25 (255.255.255.128)
- Operations: /25 (255.255.255.128)

---

## 4. Documentation:

### IP Address Ranges:
- Finance: 10.0.0.0 - 10.0.0.63
- Human Resources: 10.0.0.64 - 10.0.0.95
- Sales: 10.0.0.96 - 10.0.0.191
- Marketing: 10.0.0.192 - 10.0.0.255
- IT: 10.0.1.0 - 10.0.1.127
- Operations: 10.0.1.128 - 10.0.1.255

### Purpose:
- **Finance**: Financial transactions and accounting systems.
- **Human Resources**: Employee data and payroll systems.
- **Sales**: Customer relationship management (CRM) and sales data.
- **Marketing**: Marketing campaigns and analytics.
- **IT**: Network infrastructure and servers.
- **Operations**: Production and supply chain management.

---

## 5. Troubleshooting Scenarios:

### Connectivity Issues:
- Check routing tables for correct subnet routes.
- Verify firewall rules for inter-subnet communication.

### IP Conflicts:
- Use DHCP server logs to identify conflicting IP addresses.
- Manually assign IP addresses to resolve conflicts.

### Overlapping:
- Ensure each subnet has a unique IP address range.
- Adjust subnet masks to avoid overlapping ranges.

---

## 6. Future Growth:

### Expand Subnets:
- Increase subnet sizes by adjusting subnet masks.
- Add new subnets for additional departments or teams.

### Modify Documentation:
- Update IP address ranges and subnet masks accordingly.
- Keep track of changes for future reference.

---

## 7. Optimization:

### Efficient Routing:
- Implement routing protocols to optimize traffic between subnets.
- Use VLANs to segment traffic within departments.

### IP Address Use:
- Implement DHCP for dynamic IP address assignment.
- Reserve static IP addresses for critical devices and servers.

# SOLUTION:

### 1. **Identify Subnet Requirements**
   - **Departments**: Finance, Human Resources, Sales, Marketing, IT, Operations
   - **Future Growth**: 50% growth in each department over the next 5 years
   - **Network Topology**: Centralized data center, separate floors for each department

**Critical Thinking Questions**:
- **Why do we need a subnet for each department?**
  - Subnetting helps organize the network logically by department, allows for easier traffic management, and provides scalability.

- **How does future growth affect the subnet plan?**
  - The 50% growth in departments means that the network needs to allocate sufficient IP addresses now to avoid needing complete reconfiguration later. Planning for this growth will require choosing appropriate subnet masks to accommodate the future need.

### 2. **Allocate IP Addresses**

   - Finance: 50 hosts (needs 75 hosts with growth → **/25 subnet**)
   - Human Resources: 30 hosts (needs 45 hosts with growth → **/26 subnet**)
   - Sales: 70 hosts (needs 105 hosts with growth → **/25 subnet**)
   - Marketing: 40 hosts (needs 60 hosts with growth → **/26 subnet**)
   - IT: 100 hosts (needs 150 hosts with growth → **/24 subnet**)
   - Operations: 80 hosts (needs 120 hosts with growth → **/25 subnet**)

**Critical Thinking Questions**:
- **Why are specific subnet sizes selected?**
  - Each department's subnet is selected based on the current host count and future growth. For example, Finance needs 50 hosts, but with a 50% increase in the next five years, it would require at least 75 hosts, making a /25 subnet appropriate.

- **Why would IT require a larger subnet?**
  - IT typically manages critical network infrastructure and may need more addresses for servers, network devices, and additional systems, especially when planning for future growth and potential expansion of services.

### 3. **Subnet Masking**

   The subnet masks chosen are:

   - **/25** for 100 hosts (126 usable IPs)
   - **/26** for 50 hosts (62 usable IPs)
   - **/27** for 30 hosts (30 usable IPs)

**Critical Thinking Questions**:
- **Why is a specific subnet mask used for each department?**
  - Subnet masks are chosen to ensure enough usable IP addresses for both current and future growth. For example, Finance with 50 current hosts uses a /26 subnet (62 usable IPs), but considering growth, it may need a /25 (126 usable IPs).

### 4. **Documentation**

   Documenting IP address ranges per subnet ensures clarity and structure within the network. For example:
   - Finance: 10.0.0.0 - 10.0.0.63 (64 addresses with /26)
   - IT: 10.0.1.0 - 10.0.1.127 (128 addresses with /25)

**Critical Thinking Questions**:
- **Why is proper documentation important?**
  - Proper documentation ensures that network administrators can easily identify IP ranges, subnets, and departments. It also helps in troubleshooting and maintaining consistency, especially during network growth.

### 5. **Troubleshooting Scenarios**

   **Connectivity Issues**: If routing between subnets fails, checking the routing tables for misconfigured or missing routes ensures correct inter-subnet communication.

   **IP Conflicts**: IP conflicts can disrupt network services, and using DHCP server logs can help track down conflicting addresses.

   **Overlapping IP Ranges**: Overlapping ranges cause routing issues. Ensuring each department has a unique range avoids confusion in network routing.

**Critical Thinking Questions**:
- **Why is subnet range overlap problematic?**
  - Overlap in IP ranges causes routing confusion because the same IP address can appear in multiple places, leading to network disruptions and issues with packet delivery.

- **How does DHCP help prevent IP conflicts?**
  - DHCP dynamically assigns IP addresses, reducing the chances of overlap or conflicts. If conflicts arise, DHCP logs can help trace and resolve them.

### 6. **Future Growth**

   Future growth requires re-assessment of subnet sizes. Expanding existing subnets or adding new subnets for emerging teams may involve modifying subnet masks, adjusting IP address ranges, and ensuring scalability for new users or systems.

**Critical Thinking Questions**:
- **How should network growth be handled in terms of subnets?**
  - By selecting larger subnets upfront (considering future growth) or splitting larger address blocks for additional departments, the network can scale more efficiently without major reconfigurations.

### 7. **Optimization**

   **Efficient Routing**: Implementing routing protocols like OSPF (Open Shortest Path First) or EIGRP (Enhanced Interior Gateway Routing Protocol) helps optimize inter-subnet traffic and ensures efficient routing.

   **VLANs**: VLANs (Virtual Local Area Networks) allow for further traffic segmentation without needing additional physical networks, providing enhanced security and management.

   **DHCP**: Using DHCP ensures efficient and automated IP address allocation, reducing manual administrative overhead.

**Critical Thinking Questions**:
- **Why implement VLANs in conjunction with subnets?**
  - VLANs add an extra layer of traffic management by isolating departmental traffic logically, even though they might share the same physical network infrastructure.

- **How does routing affect network performance?**
  - Proper routing ensures that traffic flows optimally between subnets, reducing bottlenecks and ensuring that data is delivered efficiently across departments.
