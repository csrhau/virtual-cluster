# Schedules a download of the specified artefact.
# Args: name, Version major/minor/patch, file extension
define REQUIRE_IMPL
all: $1-$2.$3.$4.$5
$1-$2.$3.$4.$5: VERSION_MAJOR=$2
$1-$2.$3.$4.$5: VERSION_MINOR=$3
$1-$2.$3.$4.$5: VERSION_PATCH=$4
DOWNLOADS += $1-$2.$3.$4.$5
endef

define REQUIRE_OMPI
$(call REQUIRE_IMPL,openmpi,$1,$2,$3,tar.gz)
endef

define REQUIRE_MPICH
$(call REQUIRE_IMPL,mpich,$1,$2,$3,tar.gz)
endef

define REQUIRE_GCC
$(call REQUIRE_IMPL,gcc,$1,$2,$3,tar.gz)
endef

define REQUIRE_SLURM
$(call REQUIRE_IMPL,slurm,$1,$2,$3,tar.bz2)
endef

# Download Prerequisites
$(eval $(call REQUIRE_SLURM,17,11,7))
$(eval $(call REQUIRE_GCC,7,2,0))
$(eval $(call REQUIRE_GCC,6,3,0))
$(eval $(call REQUIRE_GCC,5,4,0))
$(eval $(call REQUIRE_OMPI,3,0,1))
$(eval $(call REQUIRE_OMPI,2,1,3))
$(eval $(call REQUIRE_OMPI,1,10,2))
$(eval $(call REQUIRE_OMPI,1,8,8))
$(eval $(call REQUIRE_MPICH,3,2,1))

CURL= curl -sL

GCC_REMOTE = ftp://ftp.gnu.org/gnu/gcc/
OPENMPI_REMOTE = https://download.open-mpi.org/release/open-mpi
MPICH_REMOTE = http://www.mpich.org/static/downloads
SLURM_REMOTE = https://download.schedmd.com/slurm

gcc-%:
	$(CURL) -o $@ $(GCC_REMOTE)/gcc-$(VERSION_MAJOR).$(VERSION_MINOR).$(VERSION_PATCH)/$@

openmpi-%:
	$(CURL) -o $@ $(OPENMPI_REMOTE)/v$(VERSION_MAJOR).$(VERSION_MINOR)/$@

mpich-%:
	$(CURL) -o $@ $(MPICH_REMOTE)/$(VERSION_MAJOR).$(VERSION_MINOR).$(VERSION_PATCH)/$@

slurm-%:
	$(CURL) -o $@ $(SLURM_REMOTE)/$@

.PHONY: all clean
.DEFAULT: all
all:
	sha1sum -c sha1sums

clean:
	$(RM) $(DOWNLOADS)
