# Awesome-Open-Table-Formats

# Top Open Table Formats Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on ACID Transactions, Schema Evolution & Multi-Engine Interoperability*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Open Table Formats**. These tools add database-like guarantees — ACID transactions, schema evolution, time travel, and hidden partitioning — on top of cheap object storage like S3, GCS, or HDFS. They are the metadata layer that turns a data lake into a lakehouse, letting Spark, Trino, Flink, and Snowflake all read the same table without copying data.

**Examples** include Apache Iceberg, Delta Lake, Apache Hudi, Apache Paimon, Apache XTable, and Project Nessie (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, cross-engine compatibility, and transparent metadata management — ideal for data engineers building lakehouse architectures who want to avoid vendor lock-in on the metadata layer that defines their tables.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **Databricks** — The managed platform anchored by Delta Lake, offering Unity Catalog governance, Photon engine acceleration, and multi-statement transactions across both Delta and Iceberg tables [citation:13]. **Best for organizations already standardized on Spark** and wanting a fully managed lakehouse with the largest Delta Lake ecosystem.

- **Snowflake** — Cloud data warehouse with native Iceberg table support and the open-sourced Polaris catalog. Lets Snowflake query Iceberg tables directly without ingestion [citation:15]. **Best for Snowflake-first teams** wanting open table format interoperability.

- **AWS Lake Formation** — Managed governance layer for S3-based data lakes, now supporting Iceberg tables natively through S3 Tables. Provides fine-grained access control and audit logging [citation:15].

- **Google BigQuery** — Supports managed Iceberg tables alongside native BigQuery storage, enabling open-format lakehouse patterns within GCP [citation:15].

## Open-Source GitHub Projects

- **[Apache Iceberg](https://github.com/apache/iceberg)**  
  **The open standard for multi-engine table interoperability** — Apache 2.0 licensed, governed neutrally by the Apache Software Foundation [citation:15]. **The broadest engine support**: Spark, Trino, Flink, PrestoDB, Hive, and more read the same table without conversion. **Delivers the lowest-latency analytical queries and most efficient storage footprint** in a 2026 IEEE benchmark covering ingestion, query performance, and compaction behavior [citation:1]. **The REST catalog specification has become a de facto standard**, with implementations like Lakekeeper providing a secure, Apache-licensed catalog server based on `apache/iceberg-rust` [citation:14]. **Adoption momentum is unmistakable**: Databricks acquired Tabular (founded by Iceberg's Netflix creators) for over a billion dollars, AWS shipped S3 Tables with native Iceberg support, Snowflake made Iceberg tables GA and open-sourced Polaris, and BigQuery added managed Iceberg tables [citation:15]. **Best for teams prioritizing engine neutrality and storage efficiency** — if you might query the same data from Spark today and Trino tomorrow, Iceberg is the safe default.

- **[Delta Lake](https://github.com/delta-io/delta)**  
  **The Spark-native format with the largest installed base** — Apache 2.0 licensed, anchored by Databricks [citation:15]. **Strongest support for ML reproducibility and governance-oriented workflows** in the 2026 IEEE automotive benchmark [citation:1]. **Delta Lake is the most optimal architecture for systems where the priority is the speed of loading data of any volume** in a separate 2026 arXiv study comparing Hudi, Iceberg, and Delta . **Multi-statement transactions** are now generally available across both Delta Lake and Apache Iceberg tables, enabling atomic multi-step warehouse workloads on the lakehouse without moving data to a separate warehouse system [citation:13]. **The Rust-based `delta-rs`** provides native bindings for Python and other languages beyond the JVM [citation:2]. **Backward compatibility is guaranteed** — newer versions always read older tables, though forward compatibility may break as protocol features are added [citation:9]. **Best for Spark-centric stacks and Databricks deployments** where the ecosystem is already Delta-native.

- **[Apache Hudi](https://github.com/apache/hudi)**  
  **The streaming and CDC specialist** — Apache 2.0 licensed, 6,000+ GitHub stars [citation:3]. **Best suited for real-time, CDC-intensive ingestion** in the 2026 IEEE automotive benchmark [citation:1]. **Hudi 1.2** introduced native `VECTOR`, `BLOB`, and `VARIANT` data types, unifying multimodal data — structured records, documents, images, and embeddings — into a single transactional lakehouse table for AI-native applications . **Uber built Hudi to solve record-level mutations on S3**, and its Record Index delivers near-O(1) key lookups on trillion-row tables [citation:15]. **Robinhood cut data freshness from ~24 hours to under 15 minutes** using Kafka into Hudi with incremental processing [citation:15]. **Trade-offs**: **Hudi proved ineffective in data loading and storage evaluation tasks** in the arXiv study, though the authors note it may be effective for incremental update and streaming scenarios . **Best for upsert-heavy, streaming CDC workloads** where you need continuous data freshness rather than batch analytics.

- **[Apache Paimon](https://github.com/apache/paimon)**  
  **The streaming lakehouse format with Flink-native roots** — Apache 2.0 licensed. **Paimon 2.0.0** is the current release [citation:11]. **Designed for real-time streaming writes and reads** on object storage, with primary key tables and merge engines for upserts. **The `paimon-vector-index` project** (v0.5.0, September 2026) adds IVF-PQ and IVF-SQ vector indexing with Rust, Java, and Python bindings [citation:4]. **Best for Flink-first streaming lakehouse architectures** where continuous ingestion and low-latency queries on fresh data matter.

- **[Apache XTable](https://github.com/apache/incubator-xtable)**  
  **The omni-directional table format translator** — Apache 2.0 licensed (incubating). **Translates metadata between Delta Lake, Apache Iceberg, and Apache Hudi** so that a single physical copy of data can be read by any engine supporting any of the three formats [citation:5]. **Ships as a Spark runtime bundle** (`xtable-spark-runtime`) for incremental metadata sync [citation:5]. **v0.4.0-incubating** passed its release vote in August 2026, with the community addressing LICENSE and README issues for the next release [citation:12]. **Best for organizations with existing data in one format** that need to expose it to engines expecting another — a migration bridge rather than a format itself.

### Additional Strong Open-Source Options

- **Project Nessie** — Git-like catalog for Iceberg with branching and merging of table metadata. Enables isolated dev/test branches on production data.
- **Lakekeeper** — Apache-licensed Rust implementation of the Iceberg REST Catalog specification, with a Docker quickstart and UI [citation:14].
- **Polaris** — Snowflake's open-sourced Iceberg catalog, donated to the Apache Software Foundation.
- **Unity Catalog** — Databricks' open-sourced catalog (now with an OSS edition) providing governance across Delta and Iceberg tables [citation:6].

**Frameworks for building custom systems**: Combine **Apache Iceberg** for engine-neutral analytics with the broadest query engine support and efficient storage, **Delta Lake** for Spark-native workloads with the largest ecosystem and multi-statement transactions, **Apache Hudi** for streaming CDC and upsert-heavy pipelines, **Apache Paimon** for Flink-native streaming lakehouse, and **Apache XTable** as a bridge when existing data must be exposed across formats — to build a lakehouse metadata layer tailored to your ingestion pattern (batch vs streaming), query engine mix (Spark-only vs multi-engine), and tolerance for operational complexity.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Open table formats differ significantly in engine support, ingestion profile, and operational complexity. **Iceberg has the broadest multi-engine support and the most efficient storage footprint** [citation:1][citation:15], but its catalog layer adds operational components. **Delta Lake is the fastest for data loading across volumes**  and has the largest installed base, but its ecosystem is most mature within Spark. **Hudi excels at streaming CDC and upserts** [citation:1], but underperformed on batch loading and storage efficiency in independent testing . **Benchmarks are workload-dependent** — the IEEE automotive benchmark and arXiv study used different datasets and metrics, and vendor-published case studies may highlight best-case results [citation:15]. **XTable is a translation layer, not a format** — it solves interoperability but does not replace choosing a primary format.
- Self-hosted open-source solutions require proper catalog service deployment (REST catalog, Hive Metastore, or Nessie), object storage configuration, and monitoring of compaction and metadata growth.

---

**Made for data engineers and architects building lakehouse metadata layers that outlive any single query engine.**
Let's make open table formats more interoperable, transparent, and workload-appropriate.
