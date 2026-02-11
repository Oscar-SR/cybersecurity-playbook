# Privilege escalation

## Windows Operating Systems

Escalating privileges in Windows requires a deep understanding of its Access Control Model.

### Key Theoretical Concepts

- **Sessions**: Windows is a multi-user system, meaning multiple users can have simultaneous sessions. Each session encapsulates relevant access data, such as permissions and login characteristics.


- **Security Identifier (SID)**: Every user or security entity is assigned a unique SID (e.g., S-1-5-32-545) so the system can identify and trust them.


- **Access Tokens**: These objects describe the security context of a process or thread. Created at login, they identify the user, their groups, and specific privileges.


- **Security Descriptors (SD)**: These contain security information for "securable objects" (like files or registry keys). An SD includes the owner's SID and two types of Access Control Lists (ACLs):


    - **DACL (Discretionary ACL)**: Specifies which users or groups are allowed or denied specific access rights.


    - **SACL (System ACL)**: Controls which access attempts generate entries in the security audit logs.


- **Access Check**: This mechanism compares a user's Access Token against an object's Security Descriptor to decide if access should be granted.


- **Integrity Levels**: Introduced in Windows Vista, these labels restrict the interaction between processes of different trust levels:


    1. **Untrusted**: For anonymous processes.


    2. **Low**: Used for internet interaction (e.g., browsers); these processes are highly restricted from writing to the system or user profile.


    3. **Medium**: The default level for standard users and most objects.


    4. **High**: Reserved for administrators (requires "Run as Administrator").


    5. **System**: Reserved for the Windows kernel and core services.

## UNIX Operating Systems

Linux privilege escalation is generally considered less complex technically but follows the same functional methodology.

### Key Theoretical Concepts

- **Users and Groups**: Every user has a unique UID, and groups have a GID. The UID 0 is strictly reserved for the root (superuser).

- **Critical Files**:

    - `/etc/passwd`: Stores user configurations, including UIDs, GIDs, home directories, and default shells.

    - `/etc/shadow`: Stores encrypted passwords and is typically only readable by the root user.

- **Process Privileges**: Processes normally run with the privileges of the user who started them. However, special permissions like setuid or setgid allow a program to run with the privileges of the file's owner or group, which is a common vector for escalation.

- **User ID Types**:

    - **Real User ID**: The ID of the user who initiated the process.

    - **Effective User ID**: The ID actually used by the kernel to validate permissions. If this is changed to 0, the process gains root privileges.

    - **Saved set-user-ID**: Used when a program is configured with the setuid bit.