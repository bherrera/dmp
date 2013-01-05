cmake_minimum_required(VERSION 2.8)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${PROJECT_SOURCE_DIR})
include_directories(${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base)
include_directories(${THIRD_PARTY_DIR}/tcmalloc/chromium/src)

set(TCMALLOC_SRCS ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/config.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/config_linux.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/config_win.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/abort.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/abort.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/arm_instruction_set_select.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/atomicops-internals-arm-generic.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/atomicops-internals-arm-v6plus.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/dynamic_annotations.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/elf_mem_image.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/linuxthreads.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/linuxthreads.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/logging.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/logging.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/low_level_alloc.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/low_level_alloc.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/spinlock.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/spinlock.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/spinlock_internal.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/spinlock_internal.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/synchronization_profiling.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/sysinfo.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/sysinfo.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/thread_lister.c 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/thread_lister.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/vdso_support.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/base/vdso_support.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/central_freelist.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/central_freelist.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/common.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/common.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/debugallocation.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/deep-heap-profile.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/deep-heap-profile.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/free_list.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/free_list.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/heap-checker-bcad.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/heap-checker.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/heap-profile-table.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/heap-profile-table.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/heap-profiler.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/internal_logging.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/internal_logging.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/linked_list.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/malloc_extension.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/malloc_hook-inl.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/malloc_hook.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/maybe_threads.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/maybe_threads.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/memory_region_map.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/memory_region_map.h
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/page_heap.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/page_heap.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/profile-handler.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/profile-handler.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/profiledata.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/profiledata.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/profiler.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/raw_printer.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/raw_printer.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/sampler.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/sampler.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/span.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/span.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/stack_trace_table.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/stack_trace_table.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/stacktrace.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/static_vars.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/static_vars.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/symbolize.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/symbolize.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/system-alloc.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/system-alloc.h 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/tcmalloc.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/thread_cache.cc 
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/thread_cache.h
#  base/allocator/allocator_shim.cc 
#  base/allocator/allocator_shim.h 
#  base/allocator/debugallocation_shim.cc
)

set(ALLOCATOR_EXTENSION_THUNKS_SRCS base/allocator/allocator_extension_thunks.cc
  base/allocator/allocator_extension_thunks.h)

set(TYPE_PROFILE_SRCS base/allocator/type_profiler.cc
  base/allocator/type_profiler.h
  base/allocator/type_profiler_control.h)

set(TYPE_PROFILER_TCMALLOC_SRCS base/allocator/type_profiler_tcmalloc.cc
  base/allocator/type_profiler_tcmalloc.h
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/gperftools/type_profiler_map.h
  ${THIRD_PARTY_DIR}/tcmalloc/chromium/src/type_profiler_map.cc)

IF(linux_keep_shadow_stacks)
#'sources': [
#  '<(tcmalloc_dir)/src/linux_shadow_stacks.cc',
#  '<(tcmalloc_dir)/src/linux_shadow_stacks.h',
#  '<(tcmalloc_dir)/src/stacktrace_shadow-inl.h',
#],
#'cflags': [
#  '-finstrument-functions',
#],
#'defines': [
#  'KEEP_SHADOW_STACKS',
#],
ENDIF(linux_keep_shadow_stacks)

IF(NOT linux_use_heapchecker)
# Do not compile and link the heapchecker source.
#'sources!': [
#  '<(tcmalloc_dir)/src/heap-checker-bcad.cc',
#  '<(tcmalloc_dir)/src/heap-checker.cc',
#],
# Disable the heap checker in tcmalloc.
#'defines': [
#  'NO_HEAP_CHECK',
# ],
ENDIF(NOT linux_use_heapchecker)

IF(use_vtable_verify)
  add_definitions(-fvtable-verify=preinit)
ENDIF(use_vtable_verify)

#add_definitions(-frtti -gline-tables-only -fintercept-allocation-functions)
add_definitions(-frtti -gline-tables-only -Wno-sign-compare -Wno-unused-result)
add_definitions(-Wno-non-literal-null-conversion)

add_library(allocator STATIC ${TCMALLOC_SRCS})
target_link_libraries(allocator type_profile_tcmalloc)

remove_definitions(-Wno-sign-compare -Wno-unused-result)
add_library(allocator_extension_thunks STATIC ${ALLOCATOR_EXTENSION_THUNKS_SRCS})

#remove_definitions(-fintercept-allocation-functions)
add_library(type_profile STATIC ${TYPE_PROFILE_SRCS})
add_library(type_profile_tcmalloc STATIC ${TYPE_PROFILER_TCMALLOC_SRCS})

