# 8. Scalability and Extensibility

The pipeline is designed so V2 can add features without rewriting the
core analysis engine.

Examples:

  -----------------------------------------------------------------------
  Future feature                      Primary change
  ----------------------------------- -----------------------------------
  native `.journal` support           new decoder

  `journalctl -o json` support        new decoder

  compressed evidence bundles         new stream reader / input adapter

  additional rule families            finding engine and classifier
                                      updates

  timeline or SARIF output            new renderer

  systemd unit snapshot analysis      new decoder and/or additional
                                      normalization path
  -----------------------------------------------------------------------

The canonical event and finding contracts are intended to remain stable
across such changes.

------------------------------------------------------------------------

