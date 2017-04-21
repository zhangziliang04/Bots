# CMake ��Ͱ汾��Ҫ��
cmake_minimum_required (VERSION 3.0)

# ��CMakeLists.txt�ļ��Ŀ�ͷ�������Ӽ���SET�﷨��
# �� CMake ֧�� gdb ������Ҳ�����ף�ֻ��Ҫָ�� Debug ģʽ�¿��� -g ѡ�
set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")

# ��Ŀ��Ϣ
project (ChatScript_Main)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# ����ͷ�ļ�Ŀ¼INCLUDE_DIRECTORIES
include_directories(./ChatScript/include /data/data_151/work_home/heyunchao/Libs/curl/include)

# ����math��Ŀ¼
# ʹ������ add_subdirectory ָ������Ŀ����һ����Ŀ¼ math������ math Ŀ¼�µ� CMakeLists.txt �ļ���Դ����Ҳ�ᱻ����
link_directories("./ChatScript" "/data/data_151/work_home/heyunchao/Libs/curl/lib/")

# ָ������Ŀ��
add_executable(ChatScript_Main Dialog.cpp Dialog.h test_Dialog.cpp)

SET (LIBHELLO_SRC Dialog.cpp Dialog.h)
ADD_LIBRARY (DialogStatic STATIC ${LIBHELLO_SRC})
ADD_LIBRARY (DialogShared SHARED ${LIBHELLO_SRC})

# �������ӿ�
# ʹ������ target_link_libraries ָ����ִ���ļ� main ��Ҫ����һ����Ϊ MathFunctions �����ӿ�
target_link_libraries(ChatScript_Main ChatScript curl)
target_link_libraries(DialogStatic ChatScript)