<!-- loio069179d957b345e1bbf3f43da31fa446 -->

# CL\_BALI\_LOG\_DB \(Interface IF\_BALI\_LOG\_DB\)

Class `CL_BALI_LOG_DB` handles all database accesses of the application logs. This includes the reading of one or several logs from the database, writing a log to the database and deleting a log from the database. In addition, it offers methods to set and clear an SAP enqueue on a log. The public interface of the instance methods is `IF_BALI_LOG_DB`.

**Public Methods**



Get an Instance of the Database Handler:

<a name="loio069179d957b345e1bbf3f43da31fa446__table_g5t_khb_xlb"/>**GET\_INSTANCE \(static\)**


<table>
<tr>
<th>

Name



</th>
<th>

Description



</th>
</tr>
<tr>
<td colspan="2">

**Returning parameter**



</td>
</tr>
<tr>
<td>

DB\_HANDLER



</td>
<td>

Database handler object: A reference to interface IF\_BALI\_LOG\_DB



</td>
</tr>
</table>



Load a single log from the database into the memory:

<a name="loio069179d957b345e1bbf3f43da31fa446__table_pyx_h3b_xlb"/>**LOAD\_LOG**


<table>
<tr>
<th>

Name



</th>
<th>

Description



</th>
</tr>
<tr>
<td colspan="2">

**Importing parameters**



</td>
</tr>
<tr>
<td>

HANDLE



</td>
<td>

Handle of the Application Log which shall be read



</td>
</tr>
<tr>
<td>

READ\_ONLY\_HEADER



</td>
<td>

\(Optional\): If set, only the header of the log is read \(no items\)

Default: Not set



</td>
</tr>
<tr>
<td colspan="2">

**Returning parameter**



</td>
</tr>
<tr>
<td>

LOG



</td>
<td>

Log which was read from the database: Reference to interface IF\_BALI\_LOG



</td>
</tr>
<tr>
<td colspan="2">

**Exceptions \(inherit from CX\_BALI\_RUNTIME\)**



</td>
</tr>
<tr>
<td>

CX\_BALI\_NOT\_FOUND



</td>
<td>

-   The log handle is initial

-   The log was not found in the database




</td>
</tr>
<tr>
<td>

CX\_BALI\_NOT\_POSSIBLE



</td>
<td>

-   ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>OBJECT\_NOT\_ALLOWED:

    Access to the log object is not allowed

-   ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>NO\_AUTHORIZATION:

    No authorization to access the log




</td>
</tr>
<tr>
<td>

CX\_BALI\_INTERNAL\_ERROR



</td>
<td>

Internal error during processing



</td>
</tr>
</table>

> ### Note:  
> The following authorization is checked:
> 
> Authorization Object: S\_APPL\_LOG with:
> 
> -   ALG\_OBJECT: Object name of the application log
> 
> -   ALG\_SUBOBJ: Subobject of the application log
> 
> -   ACTVT: 03



Load several logs via a filter from the database into the memory:

<a name="loio069179d957b345e1bbf3f43da31fa446__table_xkf_sjb_xlb"/>**LOAD\_LOGS\_VIA\_FILTER**


<table>
<tr>
<th>

Name



</th>
<th>

Description



</th>
</tr>
<tr>
<td colspan="2">

**Importing parameters**



</td>
</tr>
<tr>
<td>

FILTER



</td>
<td>

Log filter object: Reference to interface IF\_BALI\_LOG\_FILTER



</td>
</tr>
<tr>
<td>

READ\_ONLY\_HEADER



</td>
<td>

\(Optional\): If set, only the headers of the logs are read \(no items\)

Default: Not set



</td>
</tr>
<tr>
<td colspan="2">

**Returning parameter**



</td>
</tr>
<tr>
<td>

LOG\_TABLE



</td>
<td>

Table of logs which were read from the database: Table of references to interface IF\_BALI\_LOG



</td>
</tr>
<tr>
<td colspan="2">

**Exceptions \(inherit from CX\_BALI\_RUNTIME\)**



</td>
</tr>
<tr>
<td>

CX\_BALI\_NOT\_FOUND



</td>
<td>

No log can be returned which fits to the filter criteria



</td>
</tr>
<tr>
<td>

CX\_BALI\_INVALID\_PARAMETERS



</td>
<td>

-   The filter contains invalid values

-   The filter is initial or empty




</td>
</tr>
<tr>
<td>

CX\_BALI\_INTERNAL\_ERROR



</td>
<td>

Internal error during processing



</td>
</tr>
</table>

> ### Note:  
> The following authorization is checked:
> 
> Authorization Object: S\_APPL\_LOG with:
> 
> -   ALG\_OBJECT: Object name of the application log
> 
> -   ALG\_SUBOBJ: Subobject of the application log
> 
> -   ACTVT: 03
> 
> 
> If the object of a log is not allowed or if the log does not pass the authorization check, it is removed from the table of logs which is returned. An exception is only raised, if the final table is empty.



Save a single log to the database:

<a name="loio069179d957b345e1bbf3f43da31fa446__table_tgj_wkb_xlb"/>**SAVE\_LOG**


<table>
<tr>
<th>

Name



</th>
<th>

Description



</th>
</tr>
<tr>
<td colspan="2">

**Importing parameters**



</td>
</tr>
<tr>
<td>

LOG



</td>
<td>

Log which shall be saved: Reference to interface IF\_BALI\_LOG



</td>
</tr>
<tr>
<td>

USE\_2ND\_DB\_CONNECTION



</td>
<td>

\(Optional\): If set, use 2nd database connection for saving

Default: Not set



</td>
</tr>
<tr>
<td>

ASSIGN\_TO\_CURRENT\_APPL\_JOB



</td>
<td>

\(Optional\): If set, and if the application runs in an application job, a connection between the application log and an application job is established

Default: Not set



</td>
</tr>
<tr>
<td colspan="2">

**Exceptions \(inherit from CX\_BALI\_RUNTIME\)**



</td>
</tr>
<tr>
<td>

CX\_BALI\_NOT\_POSSIBLE



</td>
<td>

-   ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>OBJECT\_NOT\_ALLOWED:

    Access to the log object is not allowed

-   ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>SAVE\_NOT\_ALLOWED:

    -   Log object and log subobject are empty

    -   Locking of the log is not possible

    -   Error during saving into the database




</td>
</tr>
<tr>
<td>

CX\_BALI\_INTERNAL\_ERROR



</td>
<td>

Internal error during processing



</td>
</tr>
</table>

> ### Note:  
> -   If a second database connection is used to save the log, a commit is executed on this connection after the saving.
> 
> -   If parameter LOG is initial, the method returns without exception.



Delete a single log from the database:

<a name="loio069179d957b345e1bbf3f43da31fa446__table_a11_tlb_xlb"/>**DELETE\_LOG**


<table>
<tr>
<th>

Name



</th>
<th>

Description



</th>
</tr>
<tr>
<td colspan="2">

**Importing parameters**



</td>
</tr>
<tr>
<td>

LOG



</td>
<td>

Log which shall be saved: Reference to interface IF\_BALI\_LOG



</td>
</tr>
<tr>
<td colspan="2">

**Exceptions \(inherit from CX\_BALI\_RUNTIME\)**



</td>
</tr>
<tr>
<td>

CX\_BALI\_NOT\_POSSIBLE



</td>
<td>

-   ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>OBJECT\_NOT\_ALLOWED:

    Access to the log object is not allowed

-   ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>NO\_AUTHORIZATION:

    No authorization to access the log




</td>
</tr>
<tr>
<td>

CX\_BALI\_NOT\_FOUND



</td>
<td>

The log was not found in the database



</td>
</tr>
<tr>
<td>

CX\_BALI\_INTERNAL\_ERROR



</td>
<td>

Internal error during processing



</td>
</tr>
</table>

> ### Note:  
> -   If parameter LOG is initial, the method returns without exception.
> 
> -   The following authorization is checked:
> 
>     Authorization Object: S\_APPL\_LOG with:
> 
>     -   ALG\_OBJECT: Object name of the application log
> 
>     -   ALG\_SUBOBJ: Subobject of the application log
> 
>     -   ACTVT: 06



Set an SAP enqueue on a log:

<a name="loio069179d957b345e1bbf3f43da31fa446__table_s4p_jmb_xlb"/>**ENQUEUE**


<table>
<tr>
<th>

Name



</th>
<th>

Description



</th>
</tr>
<tr>
<td colspan="2">

**Importing parameters**



</td>
</tr>
<tr>
<td>

LOG



</td>
<td>

Log which shall be saved: Reference to interface IF\_BALI\_LOG



</td>
</tr>
<tr>
<td colspan="2">

**Exceptions \(inherit from CX\_BALI\_RUNTIME\)**



</td>
</tr>
<tr>
<td>

CX\_BALI\_NOT\_POSSIBLE



</td>
<td>

-   ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>OBJECT\_NOT\_ALLOWED:

    Access to the log object is not allowed

-   ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>ENTRY\_IS\_LOCKED:

    The enqueue cannot be set, because the log is already locked




</td>
</tr>
<tr>
<td>

CX\_BALI\_INTERNAL\_ERROR



</td>
<td>

Internal error during processing



</td>
</tr>
</table>

> ### Note:  
> If parameter LOG is initial, the method returns without exception.



Clear an SAP enqueue from a log:

<a name="loio069179d957b345e1bbf3f43da31fa446__table_jl2_5mb_xlb"/>**DEQUEUE**


<table>
<tr>
<th>

Name



</th>
<th>

Description



</th>
</tr>
<tr>
<td colspan="2">

**Importing parameters**



</td>
</tr>
<tr>
<td>

LOG



</td>
<td>

Log which shall be saved: Reference to interface IF\_BALI\_LOG



</td>
</tr>
<tr>
<td colspan="2">

**Exceptions \(inherit from CX\_BALI\_RUNTIME\)**



</td>
</tr>
<tr>
<td>

CX\_BALI\_NOT\_POSSIBLE



</td>
<td>

ERROR\_CODE: CX\_BALI\_NOT\_POSSIBLE=\>OBJECT\_NOT\_ALLOWED:

Access to the log object is not allowed



</td>
</tr>
<tr>
<td>

CX\_BALI\_INTERNAL\_ERROR



</td>
<td>

Internal error during processing



</td>
</tr>
</table>

> ### Note:  
> If parameter LOG is initial, the method returns without exception.
