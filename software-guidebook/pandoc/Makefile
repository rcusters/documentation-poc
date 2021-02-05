####################################################################################################
# Configuration
####################################################################################################

# Build configuration
BUILD_DIR = build
OUTPUT_FILE = software-guidebook

# Content configuration
CONTENT_DIR = '..'
CONTENT_FILES = $(CONTENT_DIR)/01-context/context.md\
 $(CONTENT_DIR)/02-functional-overview/functional-overview.md\
 $(CONTENT_DIR)/03-quality-attributes/quality-attributes.md
IMAGES = $(shell find $(CONTENT_DIR)/images -type f)

# Pandoc configuration
PANDOC_COMMAND = pandoc
CONTENT = awk 'FNR==1 && NR!=1 {print "\n\n"}{print}' $(CONTENT_FILES)

TOC = --toc --toc-depth 2
#FILTER_ARGS = --filter pandoc-crossref
METADATA_ARGS = --metadata-file metadata.yml
#DEBUG_ARGS = --verbose
PANDOC_ARGS = $(TOC) $(FILTER_ARGS) $(METADATA_ARGS) $(DEBUG_ARGS)
PDF_ARGS = --template templates/template.tex --pdf-engine xelatex

# Dependencies

PDF_DEPENDENCIES = $(CHAPTERS) $(IMAGES)

####################################################################################################
# Basic actions
####################################################################################################

all:	clean pdf

clean:
	rm -rf $(BUILD_DIR)

pdf:	$(BUILD_DIR)/$(OUTPUT_FILE).pdf

$(BUILD_DIR)/$(OUTPUT_FILE).pdf:
	mkdir -p $(BUILD_DIR)
	$(CONTENT) | $(PANDOC_COMMAND) $(PANDOC_ARGS) $(PDF_ARGS) -o $(BUILD_DIR)/$(OUTPUT_FILE).pdf
	@echo "$@ was built"