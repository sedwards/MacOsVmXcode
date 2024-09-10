# Variables
SWIFTFLAGS = -Xfrontend -enable-experimental-concurrency
SWIFT = swiftc

COMMON_SRCS = \
        Common/MacOSVirtualMachineConfigurationHelper.swift \
        Common/MacOSVirtualMachineDelegate.swift \
        Common/Path.swift

INSTALL_TOOL_SRCS = \
        InstallationTool/MacOSRestoreImage.swift \
        InstallationTool/MacOSVirtualMachineInstaller.swift \
        InstallationTool/main.swift

ENTITLEMENTS = ../InstallationTool.entitlements
OUTPUT_BINARY = InstallationTool-Swift

# Default target
all: $(OUTPUT_BINARY)

# Build the InstallationTool binary
$(OUTPUT_BINARY): $(COMMON_SRCS) $(INSTALL_TOOL_SRCS)
	$(SWIFT) $(SWIFTFLAGS) -framework Virtualization -o $@ $^ -import-objc-header header.h
	codesign --force --sign - -o runtime --entitlements $(ENTITLEMENTS) --timestamp=none --generate-entitlement-der $@
        
# Clean up
clean:
	rm -f $(OUTPUT_BINARY)

