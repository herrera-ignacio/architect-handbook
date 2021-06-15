# Enterprise Applications Challenges

Enterprise applications are about the display, manipulation, and storage of large amounts of often complex data and the support or automation of business processes with that data.

> Examples include reservation systems, financial systems, supply chain systems, and many others that run modern business (e.g, payroll, patient records, shipping tracking, cost analysis, credit scoring, insurance, accounting, customer service, foreign exchange trading). Enterprise applications don't include automobile fuel injection, word processors, elevator controllers, chemical plant controllers, telephone switches, operating systems, compilers, and games.

Enterprise applications have their own particular challenges and solutions, and they are different from embedded systems, control systems, telecoms, or desktop productivity software.

## Important Topics

* Layering
* Structuring domain (business) logic
* Structuring Web UI
* Linking in-memory modules to a relational database
* Handling session state in stateless environments
* Principles of distribution

## Common Concerns

Enterprise applications usually involve:

* **Persistent data**: Indeed, it usually needs to persist for several years. Also during this time, where will be many changes in the program that use it, and there'll be many changes to the structure of the data in order to store new pieces of information without disturbing the old pieces. Even if there's a fundamental change and the company installs a completely new application to handle a job, the data has to be migrated to the new application.

* **Lot of data**: So much that managing it is a major part of the system. The design and feeding of databases is a subprofession of its own.

* **Access data concurrently**: There are issues in ensuring that all of them can access the system properly and in making sure that two people don't access the same data at the same time in a way that causes errors.

* **Lot of UI screens**: Users of enterprise applications vary from ocassional to regular, and normally they will have little technical expertise. Thus, the data has to be presented lots of different ways for different purposes. Systems often have a lot of batch processing, which is easy to forget when focusing on use cases that stress user interaction.

* **Integrate with other enterprise applications**: The various systems are built at different times with different technologies, and even the collaboration mechanisms will be different, so there might be several different unified integration schemes in place at once.

* **Conceptual dissonance with the data**: Even if a company unifies the technology for integration, they run into problems with differences in business process. You may have hundreds of records in which every field can have a subtly different meaning, the sheer size of the problem becomes a challenge.

* **Complex business "illogic"**: A few one-off special use cases increase software complexity a lot. The only certain thing is that the business logic will change over time.
