#-----------------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License. See LICENSE in the project root for license information.
#-----------------------------------------------------------------------------------------

FROM swift:4

# Copy endpoint specific user setting overrides into container
COPY settings.vscode.json /root/.vscode-remote/data/User/settings.json

# Install git
RUN apt-get update && apt-get -y install git

# Install SourceKite, see https://github.com/vknabel/vscode-swift-development-environment/blob/master/README.md#installation
RUN git clone https://github.com/jinmingjian/sourcekite.git
RUN export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/swift:/usr/lib
RUN ln -s /usr/lib/libsourcekitdInProc.so /usr/lib/sourcekitdInProc
RUN cd sourcekite && swift build -Xlinker -l:sourcekitdInProc -c release

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
	