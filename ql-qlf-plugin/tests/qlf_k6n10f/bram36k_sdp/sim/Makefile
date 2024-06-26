# Copyright 2020-2022 F4PGA Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# SPDX-License-Identifier: Apache-2.0

TESTBENCH = bram36k_sdp_tb.v
POST_SYNTH = spram_36x1024_post_synth spram_32x1024_post_synth spram_18x2048_post_synth spram_16x2048_post_synth spram_9x4096_post_synth spram_8x4096_post_synth
ADDR_WIDTH = 10 10 11 11 12 12
DATA_WIDTH = 36 32 18 16 9 8
TOP = spram_36x1024 spram_32x1024 spram_18x2048 spram_16x2048 spram_9x4096 spram_8x4096
ADDR_DEFINES = $(foreach awidth, $(ADDR_WIDTH),-DADDR_WIDTH="$(awidth)")
DATA_DEFINES = $(foreach dwidth, $(DATA_WIDTH),-DDATA_WIDTH="$(dwidth)")
TOP_DEFINES = $(foreach top, $(TOP),-DTOP="$(top)")
VCD_DEFINES = $(foreach vcd, $(POST_SYNTH),-DVCD="$(vcd).vcd")

SIM_LIBS = $(shell find ../../../../qlf_k6n10f -name "*.v" -not -name "*_map.v")

define simulate_post_synth
	@iverilog  -vvvv -g2005 $(word $(1),$(ADDR_DEFINES)) $(word $(1),$(DATA_DEFINES)) $(word $(1),$(TOP_DEFINES)) $(word $(1),$(VCD_DEFINES)) -o $(word $(1),$(POST_SYNTH)).vvp $(word $(1),$(POST_SYNTH)).v $(SIM_LIBS) $(TESTBENCH) > $(word $(1),$(POST_SYNTH)).vvp.log 2>&1
	@vvp -vvvv $(word $(1),$(POST_SYNTH)).vvp > $(word $(1),$(POST_SYNTH)).vcd.log 2>&1
endef

define clean_post_synth_sim
	@rm -rf  $(word $(1),$(POST_SYNTH)).vcd $(word $(1),$(POST_SYNTH)).vvp $(word $(1),$(POST_SYNTH)).vvp.log $(word $(1),$(POST_SYNTH)).vcd.log
endef

sim:
	$(call simulate_post_synth,1)
	$(call clean_post_synth_sim,1)
	$(call simulate_post_synth,2)
	$(call clean_post_synth_sim,2)
	$(call simulate_post_synth,3)
	$(call clean_post_synth_sim,3)
	$(call simulate_post_synth,4)
	$(call clean_post_synth_sim,4)
	$(call simulate_post_synth,5)
	$(call clean_post_synth_sim,5)
	$(call simulate_post_synth,6)
	$(call clean_post_synth_sim,6)