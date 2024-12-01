- **Web security** is a major concern due to the interconnection of diverse and distributed systems.
- **Access control services** protect internet resources from unauthorized use.
- **Communication security services** ensure data confidentiality and integrity during transmission and provide non-repudiation services.

### Authentication and Access Control

- **Authentication** is crucial for access control and is typically handled by communication security services using PKI facilities.
- Current internet infrastructure **lacks mechanisms for access control at the end-user level.**
- A study by the Computer Security Institute (CSI) and FBI revealed that 71% of responders had detected unauthorized access by insiders.
- This highlights the need for **robust security management and administration** within enterprises.
- There is a need for **new or improved access control models** to address emerging security threats.

### Approaches for Web Security Models

The sources list several approaches for web security models:

- Agent-based
- Certificate-based
- Hypertext-based authorizations
- Role-based access control (RBAC)
- Mandatory access control (MAC)
- Task-based access control (TBAC)
- Discretionary access control (DAC)

### Specific Web Security Models

The sources provide detailed explanations for several specific web security models:

- **Bell-LaPadula (BLP) Model**
    
    - Focuses on **data confidentiality and controlled access** to classified information.
    - Formalizes the U.S. Department of Defense (DoD) multilevel security (MLS) policy.
    - Uses **security labels on objects and clearances for subjects** to define access control rules.
    - Built on the concept of a **state machine** with defined transition functions.
    - Defines **two mandatory access control (MAC) rules and one discretionary access control (DAC) rule**.
        - **Simple Security Property:** Prevents subjects from reading objects at higher security levels (“no read-up”).
        - ***Star Security Property:** Prevents subjects from writing to objects at lower security levels (“no write-down”).
        - **Discretionary Security Property:** Utilizes an access matrix to specify discretionary access control.
    - BLP includes **mathematical proof** that a secure system remains secure if transitions satisfy all defined properties.
    - **Limitations:** Limited applicability to systems with dynamic security levels; allows controlled copying from high to low via trusted subjects; state-transition model lacks state invariants.

- **Biba Model**
    - Developed by Kenneth J. Biba in 1975.
    - Focuses on **data integrity**.
    - Characterized by the phrase: **“no read down, no write up”**.
    - Defines security rules that are the reverse of the Bell-LaPadula rules.
        - **Invocation Property:** Prevents processes from requesting higher access; access is only allowed at equal or lower levels.
        - **Simple Integrity Axiom:** Prevents subjects from reading objects at lower integrity levels (“no read down”).
        - **Star Integrity Axiom:** Prevents subjects from writing to objects at higher integrity levels (“no write up”).

- **Clark-Wilson Model**
    
    - Provides a foundation for **specifying and analyzing integrity policies** for computing systems.
    - Based on the **concept of a transaction**, a series of operations that transition a system from one consistent state to another.
    - Focuses on the **integrity of transactions**.
    - Emphasizes **separation of duty**, requiring separate entities for transaction certification and implementation.
    - Key concepts:
        - **Constrained Data Item (CDI):** Data items with enforced integrity rules.
        - **Integrity Verification Procedure (IVP):** Ensures the validity of all CDIs in a given state.
        - **Transformation Procedure (TP):** Represents transactions that enforce integrity; transforms CDIs or UDIs while maintaining valid system states.
        - **Unconstrained Data Item (UDI):** System input that may not be trusted or constrained.
        - **Clark-Wilson triple:** Defines the relationship between an authenticated principal, programs (TPs), and data items (UDIs and CDIs).
    - **Certification Rules (C) and Enforcement Rules (E):** Nine rules ensure external and internal data integrity.
        - C1: IVP execution validates CDIs.
        - C2: TPs must transition CDIs between valid states.
        - E1: Only certified TPs can modify specific CDIs.
        - E2: Users are associated with specific TPs and CDIs, forming “allowed relations”.
        - C3: Allowed relations must adhere to separation of duty.
        - E3: User authentication is required for each TP request.
        - C4: TPs must log information for operation reconstruction.
        - C5: TPs handling UDIs must perform valid transactions for all possible UDI values.
        - E4: Only TP certifiers can modify associated entities.
    - **Clark-Wilson vs. Biba:** Clark-Wilson allows UDI to CDI conversion by specific TPs associated with users and functions, offering greater granularity compared to Biba's reliance on trusted subjects for conversion.

- **Harrison-Ruzo-Ullman (HRU) Model**
    
    - Addresses the limitations of the BLP model by defining **policies for access right changes, subject/object creation and deletion**.
    - Focuses on the **integrity of access rights**.
    - Components:
        - Set of subjects (S)
        - Set of objects (O)
        - Set of access rights (R)
        - Access matrix defining subject rights on objects

- **Chinese Wall Model**
    
    - Focuses on **conflicts of interest**.
    - Prevents users from accessing confidential information from both a client and its competitors.
    - **Dynamic access control**: Rules change based on user behavior.
    - Initially, users have no restrictions.
    - Accessing a file restricts access to competitor information.