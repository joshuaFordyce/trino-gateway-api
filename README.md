# 📉 Optimized Autoscaling for Trino (HPA/VPA)

This project provides advanced Horizontal Pod Autoscaler (HPA) and Vertical Pod Autoscaler (VPA) templates tailored for Trino's workload profile, focusing on query throughput rather than simple CPU usage.

## Key Contributions:

1.  **Queue-Depth HPA:** Uses a **Custom Metric** (e.g., `trino_queries_pending_count` scraped by Prometheus) to scale the worker fleet based on actual **demand (queue depth)**, ensuring faster response times than standard CPU-based scaling.
2.  **VPA for Right-Sizing:** Provides a template to run VPA (Vertical Pod Autoscaler) on the workers to generate optimal `requests` and `limits` recommendations. This ensures users adopt the **Guaranteed QoS** settings (`requests` == `limits`) with minimal waste.
3.  **HPA Configuration Integration:** Adds the HPA custom metric definition to the main Trino Helm Chart, allowing users to enable highly efficient autoscaling out of the box.

## PR Strategy:
Templates should be added to the Trino Helm Chart documentation and the `templates/` directory, ideally with a configuration option like `autoscaling.type: QueueDepthHPA`.