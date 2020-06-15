# testyuh

    - name: check swap full name
      shell: "lsblk -fp | grep swap | awk '{print $1}' | sed 's/^..//g'"
      register: swap_full_name
      ignore_errors: yes

    - name: swap off
      command: swapoff {{swap_full_name.stdout}}
      ignore_errors: yes
