# Global Threshold Summary

  Rule                        Threshold              Window
  --------------------------- ---------------------- --------
  AUTH_FAILURE_BURST          5 failures             5 min
  INVALID_USER_ATTEMPTS       1 / 3 events           5 min
  AUTH_FAILURE_THEN_SUCCESS   3 failures + success   15 min
  SSH_BRUTE_FORCE_PATTERN     10/1m or 25/5m         dual
  SSH_LOGIN_AFTER_FAILURES    5 failures + success   15 min
  SSH_INVALID_USER_PATTERN    3 events               5 min
  SUDO_FAILURE_BURST          3 failures             5 min
  SUDO_FAILURE_THEN_SUCCESS   2 failures + success   15 min
  SU_ATTEMPT_PATTERN          1 / 2 attempts         15 min
  SERVICE_RESTART_LOOP        3 restarts             5 min
  SELINUX_DENIAL_CLUSTER      3 denials              5 min
  APPARMOR_DENIAL_CLUSTER     3 denials              5 min
  LOGGING_GAP                 \>30 min gap           n/a
  RAPID_REBOOT_SEQUENCE       3 boots                1 hr

------------------------------------------------------------------------

This catalog intentionally favors explainable, conservative rules over
broad heuristics. Findings indicate notable behavior observed in
journald evidence; they do not assert compromise.


---

